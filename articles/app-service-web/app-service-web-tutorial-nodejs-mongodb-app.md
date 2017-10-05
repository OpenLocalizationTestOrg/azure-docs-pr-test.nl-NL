---
title: Een Node.js en MongoDB web-app in Azure bouwen | Microsoft Docs
description: Informatie over het ophalen van een Node.js-app in Azure, werken met verbinding met een Cosmos-DB-database met een verbindingsreeks voor MongoDB.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="78ef0-103">Een Node.js en MongoDB web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="78ef0-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="78ef0-104">Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="78ef0-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="78ef0-105">Deze zelfstudie laat zien hoe een Node.js-web-app in Azure maken en te verbinden met een MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="78ef0-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="78ef0-106">Wanneer u bent klaar, hebt u een gemiddelde-toepassing (MongoDB, snelle AngularJS en Node.js) wordt uitgevoerd in [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78ef0-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="78ef0-107">Voor de eenvoud, de voorbeeldtoepassing gebruikt de [MEAN.js webframework](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="78ef0-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="78ef0-109">Wat u leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="78ef0-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="78ef0-110">Maak een MongoDB-database in Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="78ef0-111">Een Node.js-app verbinden met MongoDB</span><span class="sxs-lookup"><span data-stu-id="78ef0-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="78ef0-112">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="78ef0-113">Bijwerken van het gegevensmodel en de app implementeren</span><span class="sxs-lookup"><span data-stu-id="78ef0-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="78ef0-114">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="78ef0-115">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="78ef0-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78ef0-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="78ef0-116">Prerequisites</span></span>

<span data-ttu-id="78ef0-117">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="78ef0-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="78ef0-118">Git installeren</span><span class="sxs-lookup"><span data-stu-id="78ef0-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="78ef0-119">Node.js en NPM installeren</span><span class="sxs-lookup"><span data-stu-id="78ef0-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="78ef0-120">[Installeer Gulp.js](http://gulpjs.com/) (vereist door de [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="78ef0-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="78ef0-121">Installeren en uitvoeren van MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="78ef0-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="78ef0-122">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor dit onderwerp gebruikmaken van Azure CLI versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="78ef0-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="78ef0-123">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="78ef0-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="78ef0-124">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="78ef0-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="78ef0-125">Test lokale MongoDB</span><span class="sxs-lookup"><span data-stu-id="78ef0-125">Test local MongoDB</span></span>

<span data-ttu-id="78ef0-126">Open de terminalvenster en `cd` naar de `bin` map van de MongoDB-installatie.</span><span class="sxs-lookup"><span data-stu-id="78ef0-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="78ef0-127">Alle opdrachten kunt uitvoeren in deze zelfstudie kunt u deze terminalvenster.</span><span class="sxs-lookup"><span data-stu-id="78ef0-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="78ef0-128">Voer `mongo` in de terminal verbinding maken met uw lokale MongoDB-server.</span><span class="sxs-lookup"><span data-stu-id="78ef0-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="78ef0-129">Als de verbinding geslaagd is, wordt klikt u vervolgens de MongoDB-database al uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="78ef0-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="78ef0-130">Als dit niet het geval is, zorg ervoor dat de lokale MongoDB-database is gestart door de stappen op [Installeer MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="78ef0-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="78ef0-131">Vaak MongoDB is geïnstalleerd, maar u moet nog steeds start met `mongod`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="78ef0-132">Wanneer u klaar bent test de MongoDB-database, typ `Ctrl+C` in de terminal.</span><span class="sxs-lookup"><span data-stu-id="78ef0-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="78ef0-133">Lokale Node.js-app maken</span><span class="sxs-lookup"><span data-stu-id="78ef0-133">Create local Node.js app</span></span>

<span data-ttu-id="78ef0-134">In deze stap moet u het lokale Node.js-project instellen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="78ef0-135">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="78ef0-135">Clone the sample application</span></span>

<span data-ttu-id="78ef0-136">In het terminalvenster `cd` in een werkmap.</span><span class="sxs-lookup"><span data-stu-id="78ef0-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="78ef0-137">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="78ef0-138">Deze repository voorbeeld bevat een kopie van de [MEAN.js opslagplaats](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="78ef0-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="78ef0-139">Het is gewijzigd om te worden uitgevoerd op App Service (voor meer informatie raadpleegt u de opslagplaats MEAN.js [Leesmij-bestand](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="78ef0-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="78ef0-140">De toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="78ef0-140">Run the application</span></span>

<span data-ttu-id="78ef0-141">Voer de volgende opdrachten voor het installeren van de vereiste pakketten en de toepassing niet starten.</span><span class="sxs-lookup"><span data-stu-id="78ef0-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="78ef0-142">Wanneer de app volledig wordt geladen is, ziet u iets soortgelijks als in het volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="78ef0-142">When the app is fully loaded, you see something similar to the following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="78ef0-143">Navigeer naar http://localhost: 3000 in een browser.</span><span class="sxs-lookup"><span data-stu-id="78ef0-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="78ef0-144">Klik op **aanmelden** in het bovenste menu en een testgebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="78ef0-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="78ef0-145">De MEAN.js-voorbeeldtoepassing slaat gebruikersgegevens op in de database.</span><span class="sxs-lookup"><span data-stu-id="78ef0-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="78ef0-146">Als u geslaagde in het maken van een gebruiker en aanmelden, kunnen uw app is gegevens schrijven naar de lokale MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="78ef0-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js maakt een geslaagde verbinding met MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="78ef0-148">Selecteer **Admin > artikelen beheren** sommige artikelen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="78ef0-149">Als u wilt Node.js op elk gewenst moment stoppen, drukt u op `Ctrl+C` in de terminal.</span><span class="sxs-lookup"><span data-stu-id="78ef0-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="78ef0-150">Productie MongoDB maken</span><span class="sxs-lookup"><span data-stu-id="78ef0-150">Create production MongoDB</span></span>

<span data-ttu-id="78ef0-151">In deze stap maakt u een MongoDB-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="78ef0-152">Wanneer uw app wordt geïmplementeerd naar Azure, wordt deze cloud-database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="78ef0-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="78ef0-153">Voor MongoDB, het gebruik van deze zelfstudie [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="78ef0-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="78ef0-154">MongoDB-clientverbindingen biedt ondersteuning voor cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="78ef0-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="78ef0-155">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-155">Log in to Azure</span></span>

<span data-ttu-id="78ef0-156">U gebruikt CLI Azure 2.0 om de resources te maken die nodig zijn voor het hosten van uw app in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="78ef0-157">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="78ef0-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="78ef0-158">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="78ef0-158">Create a resource group</span></span>

<span data-ttu-id="78ef0-159">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="78ef0-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="78ef0-160">In het volgende voorbeeld wordt een resourcegroep gemaakt in de regio West-Europa.</span><span class="sxs-lookup"><span data-stu-id="78ef0-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="78ef0-161">Gebruik de [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI-opdracht naar de lijst met beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="78ef0-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="78ef0-162">Een Cosmos-DB-account maken</span><span class="sxs-lookup"><span data-stu-id="78ef0-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="78ef0-163">Maak een Cosmos-DB-account met de [az cosmosdb maken](/cli/azure/cosmosdb#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="78ef0-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="78ef0-164">In de volgende opdracht te vervangen door een unieke naam van de Cosmos-database voor de  *\<cosmosdb_name >* tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="78ef0-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="78ef0-165">Deze naam wordt gebruikt als het onderdeel van het eindpunt Cosmos DB `https://<cosmosdb_name>.documents.azure.com/`, zodat de naam moet uniek zijn in alle Cosmos-DB-accounts in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="78ef0-166">De naam mag alleen kleine letters, cijfers en het koppelteken (-) en moet tussen 3 en 50 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="78ef0-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="78ef0-167">De *--kind MongoDB* parameter zorgt ervoor dat MongoDB-clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="78ef0-168">Wanneer de Cosmos-DB-account is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78ef0-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="78ef0-169">App verbinden met productie MongoDB</span><span class="sxs-lookup"><span data-stu-id="78ef0-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="78ef0-170">In deze stap maakt u verbinding maken uw voorbeeldtoepassing MEAN.js naar de Cosmos-DB-database die u zojuist hebt gemaakt, met een verbindingsreeks voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="78ef0-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="78ef0-171">De databasesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="78ef0-171">Retrieve the database key</span></span>

<span data-ttu-id="78ef0-172">Voor verbinding met de database van de Cosmos-database, moet u de databasesleutel.</span><span class="sxs-lookup"><span data-stu-id="78ef0-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="78ef0-173">Gebruik de opdracht [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) om de primaire sleutel op te halen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="78ef0-174">De Azure CLI toont informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78ef0-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Kopieer de waarde van `primaryMasterKey`. <span data-ttu-id="78ef0-176">U hebt deze informatie nodig voor de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="78ef0-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="78ef0-177">Configureer de verbindingsreeks in uw Node.js-toepassing</span><span class="sxs-lookup"><span data-stu-id="78ef0-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="78ef0-178">Open in uw opslagplaats MEAN.js _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="78ef0-179">In de `db` object, werk de waarde van `uri`:</span><span class="sxs-lookup"><span data-stu-id="78ef0-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="78ef0-180">Vervang de twee  *\<cosmosdb_name >* tijdelijke aanduidingen door de naam van uw Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="78ef0-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="78ef0-181">Vervang de  *\<primary_master_key >* aanduiding voor items met de sleutel die u in de vorige stap hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="78ef0-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="78ef0-182">De volgende code toont de `db` object:</span><span class="sxs-lookup"><span data-stu-id="78ef0-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="78ef0-183">De `ssl=true` optie is vereist omdat [Cosmos DB SSL vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="78ef0-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="78ef0-184">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="78ef0-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="78ef0-185">Test de toepassing in productiemodus</span><span class="sxs-lookup"><span data-stu-id="78ef0-185">Test the application in production mode</span></span> 

<span data-ttu-id="78ef0-186">Voer de volgende opdracht te minify en scripts voor de productie-omgeving te bundelen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="78ef0-187">Dit proces wordt gegenereerd voor de bestanden die nodig is voor de productie-omgeving.</span><span class="sxs-lookup"><span data-stu-id="78ef0-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="78ef0-188">Voer de volgende opdracht te gebruiken van de verbindingsreeks die u hebt geconfigureerd in _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="78ef0-189">`NODE_ENV=production`Hiermee stelt u de variabele voor de omgeving waarin wordt uitgelegd Node.js om uit te voeren in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="78ef0-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="78ef0-190">`node server.js`Hiermee start u de Node.js-server met `server.js` in de hoofdmap van uw opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="78ef0-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="78ef0-191">Dit is hoe uw Node.js-toepassing wordt geladen in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="78ef0-192">Wanneer de app wordt geladen, moet u controleren om ervoor te zorgen dat deze wordt uitgevoerd in de productieomgeving:</span><span class="sxs-lookup"><span data-stu-id="78ef0-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="78ef0-193">Ga naar http://localhost:8443 in een browser.</span><span class="sxs-lookup"><span data-stu-id="78ef0-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="78ef0-194">Klik op **aanmelden** in het bovenste menu en een testgebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="78ef0-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="78ef0-195">Als u geslaagde maken van een gebruiker en aanmelden, kunnen uw app is gegevens schrijven naar de database van de Cosmos-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="78ef0-196">In de terminal in stoppen Node.js `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="78ef0-197">App implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-197">Deploy app to Azure</span></span>

<span data-ttu-id="78ef0-198">In deze stap maakt implementeren u uw MongoDB verbonden Node.js-toepassing in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="78ef0-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="78ef0-199">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="78ef0-199">Create an App Service plan</span></span>

<span data-ttu-id="78ef0-200">Maak een App Service-plan met de opdracht [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="78ef0-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="78ef0-201">Het volgende voorbeeld wordt een App Service-abonnement met de naam _myAppServicePlan_ met behulp van de **vrije** prijscategorie:</span><span class="sxs-lookup"><span data-stu-id="78ef0-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="78ef0-202">Wanneer de App Service-abonnement is gemaakt, toont de Azure CLI informatie vergelijkbaar met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78ef0-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="78ef0-203">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="78ef0-203">Create a web app</span></span>

<span data-ttu-id="78ef0-204">Maak een WebApp in de `myAppServicePlan` App Service-abonnement met de [az webapp maken](/cli/azure/webapp#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="78ef0-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="78ef0-205">De web-app hebt u een hosting ruimte om uw code te implementeren en biedt een URL op voor u de gedistribueerde toepassing weergeven.</span><span class="sxs-lookup"><span data-stu-id="78ef0-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="78ef0-206">Gebruik te maken van de web-app.</span><span class="sxs-lookup"><span data-stu-id="78ef0-206">Use  to create the web app.</span></span> 

<span data-ttu-id="78ef0-207">Vervang in de volgende opdracht, de  *\<app_naam >* aanduiding voor items met een unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="78ef0-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="78ef0-208">Deze naam wordt gebruikt als het onderdeel van de standaard-URL voor de web-app zodat de naam moet uniek zijn in alle apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="78ef0-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="78ef0-209">Wanneer de web-app is gemaakt, toont de Azure CLI soortgelijke informatie als in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78ef0-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="78ef0-210">Configureren van een omgevingsvariabele</span><span class="sxs-lookup"><span data-stu-id="78ef0-210">Configure an environment variable</span></span>

<span data-ttu-id="78ef0-211">Eerder in de zelfstudie hardcoded verbinding met de database in de tekenreeks _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="78ef0-212">Aan best practice bij beveiliging wilt u deze gevoelige gegevens buiten de Git-opslagplaats te behouden.</span><span class="sxs-lookup"><span data-stu-id="78ef0-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="78ef0-213">Voor uw app in Azure wordt uitgevoerd, gebruikt u een omgevingsvariabele in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="78ef0-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="78ef0-214">In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van de [az webapp config appsettings bijwerken](/cli/azure/webapp/config/appsettings#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="78ef0-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="78ef0-215">Het volgende voorbeeld wordt een `MONGODB_URI` app-instelling in uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="78ef0-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="78ef0-216">Vervang de  *\<app_naam >*,  *\<cosmosdb_name >*, en  *\<primary_master_key >* tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="78ef0-217">In een Node.js-code, opent u deze app-instelling met `process.env.MONGODB_URI`, net zoals u toegang krijgen een omgevingsvariabele tot zou.</span><span class="sxs-lookup"><span data-stu-id="78ef0-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="78ef0-218">Nu uw wijzigingen ongedaan maken _config/env/production.js_ met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="78ef0-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="78ef0-219">Open _config/env/production.js_ opnieuw.</span><span class="sxs-lookup"><span data-stu-id="78ef0-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="78ef0-220">Denk eraan dat de standaard MEAN.js-app al is geconfigureerd voor gebruik van de `MONGODB_URI` omgevingsvariabele die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="78ef0-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="78ef0-221">Lokale Git-implementatie configureren</span><span class="sxs-lookup"><span data-stu-id="78ef0-221">Configure local git deployment</span></span> 

<span data-ttu-id="78ef0-222">Gebruik de [az webapp implementatiegebruiker ingesteld](/cli/azure/webapp/deployment/user#set) opdracht voor het maken van referenties voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="78ef0-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="78ef0-223">U kunt uw toepassing in Azure App Service op verschillende manieren, met inbegrip van de FTP-, lokale Git, Visual Studio Team Services, GitHub en BitBucket implementeren.</span><span class="sxs-lookup"><span data-stu-id="78ef0-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="78ef0-224">Voor FTP- en lokale Git is het nodig zijn voor een implementatie gebruiker geconfigureerd op de server voor verificatie van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="78ef0-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="78ef0-225">Deze gebruiker implementatie-account-niveau en verschilt van de account van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="78ef0-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="78ef0-226">Alleen moet u deze implementatie gebruiker één keer te configureren.</span><span class="sxs-lookup"><span data-stu-id="78ef0-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="78ef0-227">Vervang in de volgende opdracht *\<user-name>* en *\<password>* door een nieuwe gebruikersnaam en nieuw wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="78ef0-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="78ef0-228">De gebruikersnaam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="78ef0-228">The user name must be unique.</span></span> <span data-ttu-id="78ef0-229">Het wachtwoord moet ten minste acht tekens lang zijn en twee van de volgende drie items bevatten: letters, cijfers, symbolen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="78ef0-230">Als er een ` 'Conflict'. Details: 409`-fout optreedt, wijzigt u de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="78ef0-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="78ef0-231">Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="78ef0-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="78ef0-232">Noteer de gebruikersnaam en het wachtwoord voor gebruik in latere stappen wanneer u de app implementeert.</span><span class="sxs-lookup"><span data-stu-id="78ef0-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="78ef0-233">Gebruik de [bron in az webapp implementatie-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) opdracht voor het configureren van lokale Git-toegang tot de Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="78ef0-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="78ef0-234">Wanneer de gebruiker voor de implementatie is geconfigureerd, ziet u de implementatie-URL voor uw Azure-web-app met de Azure CLI in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="78ef0-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="78ef0-235">Kopieer de uitvoer van de terminal zoals deze wordt gebruikt in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="78ef0-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="78ef0-236">Pushen naar Azure vanaf Git</span><span class="sxs-lookup"><span data-stu-id="78ef0-236">Push to Azure from Git</span></span>

<span data-ttu-id="78ef0-237">Voeg een externe Azure-instantie toe aan uw lokale Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="78ef0-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="78ef0-238">Push naar de Azure-externe om uw Node.js-toepassing te implementeren.</span><span class="sxs-lookup"><span data-stu-id="78ef0-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="78ef0-239">U wordt gevraagd naar het wachtwoord dat u eerder hebt opgegeven als onderdeel van het maken van de implementatiegebruiker.</span><span class="sxs-lookup"><span data-stu-id="78ef0-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="78ef0-240">Azure App Service communiceert tijdens de implementatie van de voortgang met Git.</span><span class="sxs-lookup"><span data-stu-id="78ef0-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="78ef0-241">U merkt dat het implementatieproces wordt uitgevoerd [Gulp](http://gulpjs.com/) nadat `npm install`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="78ef0-242">App Service wordt niet Gulp of knorvis taken uitgevoerd tijdens de implementatie, zodat deze opslagplaats voorbeeld heeft twee extra bestanden in de hoofdmap in te schakelen:</span><span class="sxs-lookup"><span data-stu-id="78ef0-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="78ef0-243">_.Deployment_ -dit bestand vertelt App Service om uit te voeren `bash deploy.sh` als het script voor aangepaste implementatie.</span><span class="sxs-lookup"><span data-stu-id="78ef0-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="78ef0-244">_Deploy.sh_ -het script voor aangepaste implementatie.</span><span class="sxs-lookup"><span data-stu-id="78ef0-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="78ef0-245">Als u het bestand bekijkt, ziet u dat deze wordt uitgevoerd `gulp prod` nadat `npm install` en `bower install`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="78ef0-246">Deze aanpak kunt u een stap toevoegen aan uw implementatie op basis van Git.</span><span class="sxs-lookup"><span data-stu-id="78ef0-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="78ef0-247">Als u uw Azure-web-app op elk moment opnieuw opstart, wordt niet deze automatiseringstaken opnieuw uitvoeren App Service.</span><span class="sxs-lookup"><span data-stu-id="78ef0-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="78ef0-248">Blader naar de Azure-web-app</span><span class="sxs-lookup"><span data-stu-id="78ef0-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="78ef0-249">Blader naar de geïmplementeerde web-app met behulp van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="78ef0-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="78ef0-250">Klik op **aanmelden** in het bovenste menu en maak een dummy-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="78ef0-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="78ef0-251">Als u met succes voltooid zijn en de app automatisch zich bij de gebruiker aanmeldt, heeft uw MEAN.js-app in Azure verbinding met de database MongoDB (Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="78ef0-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="78ef0-253">Selecteer **Admin > artikelen beheren** sommige artikelen toevoegen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="78ef0-254">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="78ef0-254">**Congratulations!**</span></span> <span data-ttu-id="78ef0-255">U uitvoert een gegevensgestuurd Node.js-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="78ef0-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="78ef0-256">Update-gegevensmodel en de implementatie opnieuw uit</span><span class="sxs-lookup"><span data-stu-id="78ef0-256">Update data model and redeploy</span></span>

<span data-ttu-id="78ef0-257">In deze stap maakt u wijzigt de `article` data model en de wijziging van uw publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="78ef0-258">Bijwerken van het gegevensmodel</span><span class="sxs-lookup"><span data-stu-id="78ef0-258">Update the data model</span></span>

<span data-ttu-id="78ef0-259">Open _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="78ef0-260">In `ArticleSchema`, Voeg een `String` type aangeroepen `comment`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="78ef0-261">Wanneer u bent klaar, ziet uw schema-code als volgt:</span><span class="sxs-lookup"><span data-stu-id="78ef0-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-the-articles-code"></a><span data-ttu-id="78ef0-262">De code artikelen bijwerken</span><span class="sxs-lookup"><span data-stu-id="78ef0-262">Update the articles code</span></span>

<span data-ttu-id="78ef0-263">Bijwerken van de rest van uw `articles` code voor het gebruik `comment`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="78ef0-264">Er zijn vijf bestanden die u wilt wijzigen: de server-controller en de weergaven vier client.</span><span class="sxs-lookup"><span data-stu-id="78ef0-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="78ef0-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="78ef0-266">In de `update` werkt, het toevoegen van een toewijzing voor `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="78ef0-267">De volgende code toont de voltooide `update` functie:</span><span class="sxs-lookup"><span data-stu-id="78ef0-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="78ef0-268">Open _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="78ef0-269">Net boven de afsluitende `</section>` labelen, voeg de volgende regel om weer te geven `comment` samen met de rest van de artikelgegevens:</span><span class="sxs-lookup"><span data-stu-id="78ef0-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="78ef0-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="78ef0-271">Net boven de afsluitende `</a>` labelen, voeg de volgende regel om weer te geven `comment` samen met de rest van de artikelgegevens:</span><span class="sxs-lookup"><span data-stu-id="78ef0-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="78ef0-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="78ef0-273">In de `<div class="list-group">` element en net boven de afsluitende `</a>` labelen, voeg de volgende regel om weer te geven `comment` samen met de rest van de artikelgegevens:</span><span class="sxs-lookup"><span data-stu-id="78ef0-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="78ef0-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="78ef0-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="78ef0-275">Zoek de `<div class="form-group">` element met de verzendknop, welke ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="78ef0-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="78ef0-276">Net boven deze tag toevoegen `<div class="form-group">` element waarmee mensen bewerken de `comment` veld.</span><span class="sxs-lookup"><span data-stu-id="78ef0-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="78ef0-277">Uw nieuwe element moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="78ef0-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="78ef0-278">Uw wijzigingen lokaal testen</span><span class="sxs-lookup"><span data-stu-id="78ef0-278">Test your changes locally</span></span>

<span data-ttu-id="78ef0-279">Sla al uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="78ef0-279">Save all your changes.</span></span>

<span data-ttu-id="78ef0-280">Test uw wijzigingen opnieuw in de productiemodus.</span><span class="sxs-lookup"><span data-stu-id="78ef0-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="78ef0-281">Vergeet niet dat uw _config/env/production.js_ is hersteld, en de `MONGODB_URI` omgevingsvariabele wordt alleen ingesteld in uw Azure-web-app en niet op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="78ef0-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="78ef0-282">Als u het configuratiebestand bekijkt, kunt u vinden dat de productconfiguratie van de standaard voor het gebruik van een lokale MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="78ef0-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="78ef0-283">Dit zorgt ervoor dat u productiegegevens niet raken als u uw codewijzigingen lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="78ef0-284">Navigeer naar `http://localhost:8443` in een browser en zorg ervoor dat u bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="78ef0-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="78ef0-285">Selecteer **Admin > artikelen beheren**, klikt u vervolgens een artikel toevoegen door te selecteren de  **+**  knop.</span><span class="sxs-lookup"><span data-stu-id="78ef0-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="78ef0-286">U ziet de nieuwe `Comment` textbox nu.</span><span class="sxs-lookup"><span data-stu-id="78ef0-286">You see the new `Comment` textbox now.</span></span>

![Veld toegevoegde opmerking aan artikelen](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="78ef0-288">In de terminal in stoppen Node.js `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="78ef0-289">Wijzigingen publiceren naar Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-289">Publish changes to Azure</span></span>

<span data-ttu-id="78ef0-290">Uw wijzigingen in Git en vervolgens de codewijzigingen pushen naar Azure.</span><span class="sxs-lookup"><span data-stu-id="78ef0-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="78ef0-291">Eenmaal de `git push` is voltooid, gaat u naar uw Azure-web-app en de nieuwe functionaliteit uitproberen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![Model en de database-wijzigingen die zijn gepubliceerd naar Azure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="78ef0-293">Als u alle artikelen die eerder is toegevoegd, kunt u nog steeds zien.</span><span class="sxs-lookup"><span data-stu-id="78ef0-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="78ef0-294">Bestaande gegevens in uw Cosmos-database is niet verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="78ef0-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="78ef0-295">Ook de updates aan het gegevensschema en uw bestaande gegevens intact blijft.</span><span class="sxs-lookup"><span data-stu-id="78ef0-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="78ef0-296">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="78ef0-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="78ef0-297">Als uw Node.js-toepassing in Azure App Service wordt uitgevoerd, kunt u de logboeken van de console doorgesluisd naar uw terminal opvragen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="78ef0-298">Op die manier kunt u de dezelfde diagnostische berichten op te sporen toepassingsfouten ophalen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="78ef0-299">Gebruik voor het starten van de streaming-logboek de [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.</span><span class="sxs-lookup"><span data-stu-id="78ef0-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="78ef0-300">Uw Azure-web-app in de browser om op te halen van sommige webverkeer eenmaal streaming-logboek is gestart, worden vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="78ef0-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="78ef0-301">U ziet nu de logboeken van de console is doorgegeven naar de terminal.</span><span class="sxs-lookup"><span data-stu-id="78ef0-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="78ef0-302">Stop log streaming op elk gewenst moment door typen `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="78ef0-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="78ef0-303">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="78ef0-303">Manage your Azure web app</span></span>

<span data-ttu-id="78ef0-304">Ga naar de [Azure-portal](https://portal.azure.com) om te zien van de web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="78ef0-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="78ef0-305">Klik vanuit het linkermenu op **App Services** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="78ef0-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="78ef0-307">Standaard ziet u de portal voor uw web-app **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="78ef0-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="78ef0-308">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="78ef0-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="78ef0-309">Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="78ef0-310">De tabbladen aan de linkerkant van de pagina's worden weergegeven de andere configuratie dat kunt u openen.</span><span class="sxs-lookup"><span data-stu-id="78ef0-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="78ef0-312">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78ef0-312">Next steps</span></span>

<span data-ttu-id="78ef0-313">Wat u hebt geleerd:</span><span class="sxs-lookup"><span data-stu-id="78ef0-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="78ef0-314">Maak een MongoDB-database in Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="78ef0-315">Een Node.js-app verbinden met MongoDB</span><span class="sxs-lookup"><span data-stu-id="78ef0-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="78ef0-316">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="78ef0-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="78ef0-317">Bijwerken van het gegevensmodel en de app implementeren</span><span class="sxs-lookup"><span data-stu-id="78ef0-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="78ef0-318">Logboeken van de stroom van Azure naar uw terminal</span><span class="sxs-lookup"><span data-stu-id="78ef0-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="78ef0-319">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="78ef0-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="78ef0-320">Ga naar de volgende zelfstudie voor informatie over het toewijzen van een aangepaste DNS-naam aan uw web-app.</span><span class="sxs-lookup"><span data-stu-id="78ef0-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="78ef0-321">Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="78ef0-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
