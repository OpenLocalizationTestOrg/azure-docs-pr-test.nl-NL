---
title: aaaConnect een MongoDB app tooAzure Cosmos DB met behulp van Node.js | Microsoft Docs
description: Meer informatie over hoe tooconnect een bestaande app Node.js MongoDB-tooAzure Cosmos-DB
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="e334c-103">Azure Cosmos DB: een bestaande Node.js MongoDB-web-app migreren</span><span class="sxs-lookup"><span data-stu-id="e334c-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="e334c-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e334c-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e334c-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="e334c-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="e334c-106">Deze snelstartgids demonstreert hoe een bestaande toouse [MongoDB](mongodb-introduction.md) app, geschreven in Node.js en verbinding maken met het tooyour Azure DB die Cosmos-database, die ondersteuning biedt voor MongoDB-clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="e334c-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="e334c-107">Met andere woorden, kent uw Node.js-toepassing alleen er wordt verbinding gemaakt met behulp van MongoDB APIs tooa-database.</span><span class="sxs-lookup"><span data-stu-id="e334c-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="e334c-108">Is transparant toohello-toepassing die Hallo van gegevens wordt opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e334c-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="e334c-109">Als u klaar bent, beschikt u over een MEAN-toepassing (MongoDB, Express, AngularJS en Node.js) die wordt uitgevoerd op [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="e334c-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![MEAN.js-app uitgevoerd in Azure App Service](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e334c-111">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e334c-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e334c-112">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="e334c-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e334c-113">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e334c-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e334c-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e334c-114">Prerequisites</span></span> 
<span data-ttu-id="e334c-115">Bovendien tooAzure CLI, moet u [Node.js](https://nodejs.org/) en [Git](http://www.git-scm.com/downloads) lokaal toorun geïnstalleerd `npm` en `git` opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e334c-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="e334c-116">U moet bekend zijn met de basisbegrippen van Node.js.</span><span class="sxs-lookup"><span data-stu-id="e334c-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="e334c-117">Deze snelstartgids is niet bedoeld toohelp u met het ontwikkelen van Node.js-toepassingen in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="e334c-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="e334c-118">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="e334c-118">Clone hello sample application</span></span>

<span data-ttu-id="e334c-119">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="e334c-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="e334c-120">Hallo na opdrachten tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e334c-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="e334c-121">Deze voorbeeld-bibliotheek bevat standaard Hallo [MEAN.js](http://meanjs.org/) toepassing.</span><span class="sxs-lookup"><span data-stu-id="e334c-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="e334c-122">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e334c-122">Run hello application</span></span>

<span data-ttu-id="e334c-123">Vereist hello-pakketten installeren en start de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="e334c-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="e334c-124">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="e334c-124">Log in tooAzure</span></span>

<span data-ttu-id="e334c-125">Als u van een geïnstalleerde Azure CLI gebruikmaakt, meldt u zich in Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="e334c-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="e334c-126">U kunt deze stap overslaan als u hello Azure Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="e334c-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="e334c-127">Hello Azure Cosmos DB-module toevoegen</span><span class="sxs-lookup"><span data-stu-id="e334c-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="e334c-128">Als u van een geïnstalleerde Azure CLI gebruikmaakt, controleert u toosee als hello `cosmosdb` onderdeel al is geïnstalleerd door het uitvoeren van Hallo `az` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e334c-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="e334c-129">Als `cosmosdb` in lijst met opdrachten base Hallo, gaan de volgende opdracht toohello is.</span><span class="sxs-lookup"><span data-stu-id="e334c-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="e334c-130">U kunt deze stap overslaan als u hello Azure Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="e334c-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="e334c-131">Als `cosmosdb` is niet in lijst met opdrachten base Hallo, installeer [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e334c-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="e334c-132">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="e334c-132">Create a resource group</span></span>

<span data-ttu-id="e334c-133">Maak een [resourcegroep](../azure-resource-manager/resource-group-overview.md) Hello [az groep maken](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e334c-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e334c-134">Een Azure-resourcegroep is een logische container waarin Azure-resources, zoals web-apps, databases en opslagaccounts, worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="e334c-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="e334c-135">Hallo maakt volgende voorbeeld een resourcegroep in de regio West-Europa Hallo.</span><span class="sxs-lookup"><span data-stu-id="e334c-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="e334c-136">Kies een unieke naam voor de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="e334c-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="e334c-137">Als u van Azure Cloud-Shell gebruikmaakt, klikt u op **probeert het**, volg Hallo aanwijzingen toologin en Hallo-opdracht kopiëren naar het Hallo-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e334c-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="e334c-138">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="e334c-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="e334c-139">Een Azure DB die Cosmos-account maken met de Hallo [az cosmosdb maken](/cli/azure/cosmosdb#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="e334c-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="e334c-140">In Hallo opdracht, na Neem vervangen door uw eigen unieke Azure DB die Cosmos-accountnaam waar u Hallo zien `<cosmosdb-name>` tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="e334c-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="e334c-141">Deze unieke naam wordt gebruikt als onderdeel van uw Azure DB die Cosmos-eindpunt (`https://<cosmosdb-name>.documents.azure.com/`), zodat het Hallo-naam moet toobe unieke alle Azure DB die Cosmos-accounts in Azure.</span><span class="sxs-lookup"><span data-stu-id="e334c-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="e334c-142">Hallo `--kind MongoDB` parameter zorgt ervoor dat MongoDB-clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="e334c-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="e334c-143">Wanneer hello Azure DB die Cosmos-account is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="e334c-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="e334c-144">In dit voorbeeld gebruikt JSON als hello Azure CLI uitvoerindeling, Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="e334c-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="e334c-145">een andere uitvoer toouse indeling, Zie [uitvoerindelingen voor Azure CLI 2.0 opdrachten](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e334c-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="e334c-146">Verbinding maken met uw Node.js-toepassing toohello database</span><span class="sxs-lookup"><span data-stu-id="e334c-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="e334c-147">In deze stap maakt u verbinding maken uw MEAN.js toepassing tooan Azure Cosmos DB voorbeelddatabase die u zojuist hebt gemaakt, met een verbindingsreeks voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e334c-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="e334c-148">Hallo-verbindingsreeks configureren in uw Node.js-toepassing</span><span class="sxs-lookup"><span data-stu-id="e334c-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="e334c-149">Open `config/env/local-development.js` in uw MEAN.js-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e334c-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="e334c-150">Hallo-inhoud van dit bestand vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="e334c-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="e334c-151">Zorg ervoor dat tooalso vervangen Hallo twee `<cosmosdb-name>` tijdelijke aanduidingen door de naam van uw Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e334c-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="e334c-152">Hallo-sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="e334c-152">Retrieve hello key</span></span>

<span data-ttu-id="e334c-153">In de volgorde tooconnect tooan Azure DB die Cosmos-database moet u Hallo databasesleutel.</span><span class="sxs-lookup"><span data-stu-id="e334c-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="e334c-154">Gebruik Hallo [az cosmosdb lijst-sleutels](/cli/azure/cosmosdb#list-keys) opdracht tooretrieve Hallo primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="e334c-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="e334c-155">Hello Azure CLI levert informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="e334c-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="e334c-156">Hallo-waarde van kopiëren `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="e334c-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="e334c-157">Plak dit via Hallo `<primary_master_key>` in `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="e334c-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="e334c-158">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="e334c-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="e334c-159">Hallo toepassing opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e334c-159">Run hello application again.</span></span>

<span data-ttu-id="e334c-160">Voer `npm start` opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="e334c-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="e334c-161">Een consolebericht moet u nu vertellen dat die Hallo ontwikkelings-omgeving actief is.</span><span class="sxs-lookup"><span data-stu-id="e334c-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="e334c-162">Navigeer te`http://localhost:3000` in een browser.</span><span class="sxs-lookup"><span data-stu-id="e334c-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="e334c-163">Klik op **aanmelden** in de bovenste menu en probeer het toocreate Hallo twee testupdate worden uitgevoerd van gebruikers.</span><span class="sxs-lookup"><span data-stu-id="e334c-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="e334c-164">Hallo MEAN.js voorbeeldtoepassing slaat gebruikersgegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="e334c-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="e334c-165">Als u geslaagde en MEAN.js automatisch zich aanmeldt bij Hallo gebruiker gemaakt en de Azure DB die Cosmos-verbinding werkt.</span><span class="sxs-lookup"><span data-stu-id="e334c-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js verbinding maakt met succes tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="e334c-167">Gegevens bekijken in Data Explorer</span><span class="sxs-lookup"><span data-stu-id="e334c-167">View data in Data Explorer</span></span>

<span data-ttu-id="e334c-168">Gegevens die zijn opgeslagen door een Cosmos Azure DB is beschikbaar tooview query en voer bedrijfslogica ingeschakeld in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e334c-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="e334c-169">tooview, opvragen en werken met gebruikersgegevens Hallo gemaakt in Hallo vorige stap, aanmelding toohello [Azure-portal](https://portal.azure.com) in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e334c-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="e334c-170">Typ in Hallo top zoekvak Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e334c-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="e334c-171">Wanneer uw Cosmos DB-accountblade wordt geopend, selecteert u uw Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="e334c-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="e334c-172">Klik in het Hallo linkernavigatiebalk, Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="e334c-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="e334c-173">Vouw uw verzameling in hello verzamelingen deelvenster en vervolgens u kunt Hallo documenten weergeven in de verzameling hello, Hallo-gegevens opvragen, en zelfs maken en opgeslagen procedures, triggers en UDF's worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e334c-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Data Explorer in hello Azure-portal](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="e334c-175">Hallo Node.js-toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="e334c-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="e334c-176">In deze stap maakt implementeren u uw MongoDB verbonden Node.js-toepassing tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e334c-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="e334c-177">Hebt u wellicht dat Hallo-configuratiebestand dat u eerder hebt gewijzigd is voor Hallo-ontwikkelomgeving (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="e334c-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="e334c-178">Wanneer u uw toepassing tooApp Service implementeert, wordt deze standaard in de productieomgeving Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e334c-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="e334c-179">U moet nu dus toomake Hallo dezelfde toohello respectieve configuratiebestand wijzigen.</span><span class="sxs-lookup"><span data-stu-id="e334c-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="e334c-180">Open `config/env/production.js` in uw MEAN.js-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e334c-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="e334c-181">In Hallo `db` object, vervang de waarde Hallo van `uri` net als in het volgende voorbeeld Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="e334c-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="e334c-182">Worden ervoor tooreplace Hallo tijdelijke aanduidingen als voor.</span><span class="sxs-lookup"><span data-stu-id="e334c-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="e334c-183">Hallo `ssl=true` optie is belangrijk omdat [SSL is vereist voor Azure Cosmos DB](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="e334c-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="e334c-184">In terminal hello, alle uw wijzigingen in Git.</span><span class="sxs-lookup"><span data-stu-id="e334c-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="e334c-185">U kunt beide toorun opdrachten kopiëren ze samen.</span><span class="sxs-lookup"><span data-stu-id="e334c-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="e334c-186">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="e334c-186">Clean up resources</span></span>

<span data-ttu-id="e334c-187">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e334c-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="e334c-188">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e334c-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="e334c-189">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="e334c-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e334c-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e334c-190">Next steps</span></span>

<span data-ttu-id="e334c-191">In deze snelstartgids hebt u geleerd hoe een Cosmos Azure DB toocreate account en een Hallo Data Explorer met MongoDB-verzameling maken.</span><span class="sxs-lookup"><span data-stu-id="e334c-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="e334c-192">U kunt nu uw MongoDB gegevens tooAzure Cosmos DB migreren.</span><span class="sxs-lookup"><span data-stu-id="e334c-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="e334c-193">MongoDB-gegevens importeren in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e334c-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
