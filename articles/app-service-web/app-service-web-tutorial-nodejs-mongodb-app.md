---
title: een Node.js en MongoDB web-app in Azure aaaBuild | Microsoft Docs
description: Meer informatie over hoe een Node.js-app in Azure AD werkt met verbinding tooa Cosmos DB database met een verbindingsreeks MongoDB tooget.
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
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="8511d-103">Een Node.js en MongoDB web-app in Azure bouwen</span><span class="sxs-lookup"><span data-stu-id="8511d-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="8511d-104">Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service.</span><span class="sxs-lookup"><span data-stu-id="8511d-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="8511d-105">Deze zelfstudie laat zien hoe toocreate een Node.js web-app in Azure en verbinding maken met het tooa MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="8511d-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="8511d-106">Wanneer u bent klaar, hebt u een gemiddelde-toepassing (MongoDB, snelle AngularJS en Node.js) wordt uitgevoerd in [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8511d-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="8511d-107">Voor het gemak, Hallo-voorbeeldtoepassing gebruikt Hallo [MEAN.js webframework](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="8511d-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="8511d-109">Wat u leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="8511d-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8511d-110">Maak een MongoDB-database in Azure</span><span class="sxs-lookup"><span data-stu-id="8511d-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="8511d-111">Verbinding maken met een Node.js-app tooMongoDB</span><span class="sxs-lookup"><span data-stu-id="8511d-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="8511d-112">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="8511d-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="8511d-113">Hallo-gegevensmodel bijwerken en Hallo app implementeren</span><span class="sxs-lookup"><span data-stu-id="8511d-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="8511d-114">Diagnostische logboeken van de stroom van Azure</span><span class="sxs-lookup"><span data-stu-id="8511d-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="8511d-115">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8511d-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8511d-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8511d-116">Prerequisites</span></span>

<span data-ttu-id="8511d-117">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="8511d-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="8511d-118">Git installeren</span><span class="sxs-lookup"><span data-stu-id="8511d-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="8511d-119">Node.js en NPM installeren</span><span class="sxs-lookup"><span data-stu-id="8511d-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="8511d-120">[Installeer Gulp.js](http://gulpjs.com/) (vereist door de [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="8511d-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="8511d-121">Installeren en uitvoeren van MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="8511d-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8511d-122">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, wordt in dit onderwerp vereist dat u hello Azure CLI versie 2.0 of hoger worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="8511d-123">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="8511d-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8511d-124">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8511d-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="8511d-125">Test lokale MongoDB</span><span class="sxs-lookup"><span data-stu-id="8511d-125">Test local MongoDB</span></span>

<span data-ttu-id="8511d-126">Open Hallo terminalvenster en `cd` toohello `bin` map van de MongoDB-installatie.</span><span class="sxs-lookup"><span data-stu-id="8511d-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="8511d-127">U kunt deze toorun terminalvenster alle Hallo-opdrachten gebruiken in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8511d-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="8511d-128">Voer `mongo` in Hallo terminal tooconnect tooyour lokale MongoDB-server.</span><span class="sxs-lookup"><span data-stu-id="8511d-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="8511d-129">Als de verbinding geslaagd is, wordt klikt u vervolgens de MongoDB-database al uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="8511d-130">Als dit niet het geval is, zorg ervoor dat uw lokale MongoDB-database is gestart door de stappen op Hallo [Installeer MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="8511d-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="8511d-131">Vaak MongoDB is geïnstalleerd, maar u moet nog steeds toostart het door het uitvoeren van `mongod`.</span><span class="sxs-lookup"><span data-stu-id="8511d-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="8511d-132">Wanneer u klaar bent test de MongoDB-database, typ `Ctrl+C` in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="8511d-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="8511d-133">Lokale Node.js-app maken</span><span class="sxs-lookup"><span data-stu-id="8511d-133">Create local Node.js app</span></span>

<span data-ttu-id="8511d-134">In deze stap maakt instellen u lokaal Node.js-project Hallo.</span><span class="sxs-lookup"><span data-stu-id="8511d-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="8511d-135">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="8511d-135">Clone hello sample application</span></span>

<span data-ttu-id="8511d-136">In het terminalvenster hello, `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="8511d-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="8511d-137">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="8511d-138">Deze repository voorbeeld bevat een kopie van Hallo [MEAN.js opslagplaats](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="8511d-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="8511d-139">Het gewijzigde toorun op App Service is (Zie voor meer informatie, Hallo MEAN.js opslagplaats [Leesmij-bestand](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="8511d-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="8511d-140">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="8511d-140">Run hello application</span></span>

<span data-ttu-id="8511d-141">Voer Hallo opdrachten tooinstall vereist hello-pakketten te volgen en Hallo toepassing starten.</span><span class="sxs-lookup"><span data-stu-id="8511d-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="8511d-142">Wanneer de app Hallo volledig geladen is, ziet u iets dergelijks toohello volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="8511d-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="8511d-143">Toohttp://localhost:3000 in een browser navigeren.</span><span class="sxs-lookup"><span data-stu-id="8511d-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="8511d-144">Klik op **aanmelden** in Hallo bovenste menu en een testgebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="8511d-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="8511d-145">Hallo MEAN.js voorbeeldtoepassing slaat gebruikersgegevens in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="8511d-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="8511d-146">Als u geslaagde in het maken van een gebruiker en aanmelden, wordt uw app gegevens toohello lokale MongoDB-database geschreven.</span><span class="sxs-lookup"><span data-stu-id="8511d-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js verbinding maakt met succes tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="8511d-148">Selecteer **Admin > artikelen beheren** tooadd sommige artikelen.</span><span class="sxs-lookup"><span data-stu-id="8511d-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="8511d-149">Druk op toostop Node.js op elk gewenst moment `Ctrl+C` in Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="8511d-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="8511d-150">Productie MongoDB maken</span><span class="sxs-lookup"><span data-stu-id="8511d-150">Create production MongoDB</span></span>

<span data-ttu-id="8511d-151">In deze stap maakt u een MongoDB-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="8511d-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="8511d-152">Wanneer uw app geïmplementeerd tooAzure is, gebruikt deze cloud-database.</span><span class="sxs-lookup"><span data-stu-id="8511d-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="8511d-153">Voor MongoDB, het gebruik van deze zelfstudie [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="8511d-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="8511d-154">MongoDB-clientverbindingen biedt ondersteuning voor cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8511d-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="8511d-155">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="8511d-155">Log in tooAzure</span></span>

<span data-ttu-id="8511d-156">U gebruikt hello Azure CLI 2.0 toocreate Hallo benodigde resources toohost uw app in Azure.</span><span class="sxs-lookup"><span data-stu-id="8511d-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="8511d-157">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="8511d-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="8511d-158">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="8511d-158">Create a resource group</span></span>

<span data-ttu-id="8511d-159">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8511d-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="8511d-160">Hallo maakt volgende voorbeeld een resourcegroep in de regio West-Europa Hallo.</span><span class="sxs-lookup"><span data-stu-id="8511d-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="8511d-161">Gebruik Hallo [az appservice lijst-locaties](/cli/azure/appservice#list-locations) Azure CLI opdracht toolist beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="8511d-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="8511d-162">Een Cosmos-DB-account maken</span><span class="sxs-lookup"><span data-stu-id="8511d-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="8511d-163">Een Cosmos-DB-account maken met de Hallo [az cosmosdb maken](/cli/azure/cosmosdb#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8511d-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="8511d-164">In Hallo volgende opdracht, vervangt u een unieke naam van de Cosmos-DB voor Hallo  *\<cosmosdb_name >* tijdelijke aanduiding.</span><span class="sxs-lookup"><span data-stu-id="8511d-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="8511d-165">Deze naam wordt gebruikt als onderdeel van het eindpunt van de Cosmos-DB hello, Hallo `https://<cosmosdb_name>.documents.azure.com/`, zodat het Hallo-naam moet toobe unieke alle Cosmos-DB-accounts in Azure.</span><span class="sxs-lookup"><span data-stu-id="8511d-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="8511d-166">Hallo-naam mag alleen kleine letters, cijfers en Hallo koppelteken (-) en moet tussen 3 en 50 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="8511d-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="8511d-167">Hallo *--kind MongoDB* parameter zorgt ervoor dat MongoDB-clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="8511d-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="8511d-168">Wanneer Hallo Cosmos-DB-account is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8511d-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="8511d-169">Verbinding maken met app-tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="8511d-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="8511d-170">In deze stap maakt u verbinding maken uw MEAN.js toepassing toohello Cosmos DB voorbeelddatabase die u zojuist hebt gemaakt, met een verbindingsreeks voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="8511d-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="8511d-171">Hallo databasesleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="8511d-171">Retrieve hello database key</span></span>

<span data-ttu-id="8511d-172">tooconnect toohello Cosmos-DB-database, moet u Hallo databasesleutel.</span><span class="sxs-lookup"><span data-stu-id="8511d-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="8511d-173">Gebruik Hallo [az cosmosdb lijst-sleutels](/cli/azure/cosmosdb#list-keys) opdracht tooretrieve Hallo primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="8511d-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="8511d-174">Hello Azure CLI ziet u informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8511d-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Hallo-waarde van kopiëren `primaryMasterKey`. <span data-ttu-id="8511d-176">U moet deze informatie in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="8511d-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="8511d-177">Hallo-verbindingsreeks configureren in uw Node.js-toepassing</span><span class="sxs-lookup"><span data-stu-id="8511d-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="8511d-178">Open in uw opslagplaats MEAN.js _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="8511d-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="8511d-179">In Hallo `db` object, werk Hallo-waarde van `uri`:</span><span class="sxs-lookup"><span data-stu-id="8511d-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="8511d-180">Vervang Hallo twee  *\<cosmosdb_name >* tijdelijke aanduidingen door de naam van uw Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="8511d-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="8511d-181">Vervang Hallo  *\<primary_master_key >* tijdelijke aanduiding met Hallo-sleutel die u in de vorige stap Hallo hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="8511d-182">Hallo volgende code toont Hallo `db` object:</span><span class="sxs-lookup"><span data-stu-id="8511d-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="8511d-183">Hallo `ssl=true` optie is vereist omdat [Cosmos DB SSL vereist](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="8511d-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="8511d-184">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="8511d-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="8511d-185">Hallo-toepassing in de productiemodus testen</span><span class="sxs-lookup"><span data-stu-id="8511d-185">Test hello application in production mode</span></span> 

<span data-ttu-id="8511d-186">Na de opdracht toominify en de bundel scripts voor de productieomgeving Hallo Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="8511d-187">Dit proces Hallo-bestanden die nodig is voor productie-omgeving Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="8511d-188">Voer Hallo opdracht toouse Hallo verbindingsreeks u hebt geconfigureerd in volgende _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="8511d-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="8511d-189">`NODE_ENV=production`Hiermee stelt u Hallo omgevingsvariabele waarin wordt uitgelegd Node.js toorun in Hallo-productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="8511d-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="8511d-190">`node server.js`Start Hallo Node.js-server met `server.js` in de hoofdmap van uw opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="8511d-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="8511d-191">Dit is hoe uw Node.js-toepassing wordt geladen in Azure.</span><span class="sxs-lookup"><span data-stu-id="8511d-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="8511d-192">Wanneer de app hello wordt geladen, controleert u ervoor dat deze wordt uitgevoerd in de productieomgeving Hallo toomake:</span><span class="sxs-lookup"><span data-stu-id="8511d-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="8511d-193">Toohttp://localhost:8443 in een browser navigeren.</span><span class="sxs-lookup"><span data-stu-id="8511d-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="8511d-194">Klik op **aanmelden** in Hallo bovenste menu en een testgebruiker maken.</span><span class="sxs-lookup"><span data-stu-id="8511d-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="8511d-195">Als u geslaagde maken van een gebruiker en aanmelden, kunnen uw app is gegevens toohello Cosmos DB database schrijven in Azure.</span><span class="sxs-lookup"><span data-stu-id="8511d-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="8511d-196">In terminal hello, stopt u Node.js door `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="8511d-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="8511d-197">App-tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="8511d-197">Deploy app tooAzure</span></span>

<span data-ttu-id="8511d-198">In deze stap maakt implementeren u uw toepassing tooAzure voor MongoDB verbonden Node.js-App Service.</span><span class="sxs-lookup"><span data-stu-id="8511d-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="8511d-199">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="8511d-199">Create an App Service plan</span></span>

<span data-ttu-id="8511d-200">Maken van een App Service-abonnement met Hallo [az appservice-abonnement maken](/cli/azure/appservice/plan#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8511d-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="8511d-201">Hallo volgende voorbeeld maakt u een App Service-abonnement met de naam _myAppServicePlan_ met Hallo **vrije** prijscategorie:</span><span class="sxs-lookup"><span data-stu-id="8511d-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="8511d-202">Wanneer Hallo App Service-abonnement is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8511d-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="8511d-203">Een webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="8511d-203">Create a web app</span></span>

<span data-ttu-id="8511d-204">Een web-app maken in Hallo `myAppServicePlan` App Service-abonnement met Hallo [az webapp maken](/cli/azure/webapp#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8511d-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="8511d-205">Hallo web app geeft u een hosting-ruimte toodeploy uw code en biedt een URL voor u tooview Hallo toepassing geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8511d-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="8511d-206">Gebruik toocreate Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="8511d-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="8511d-207">Hallo opdracht, na Vervang in Hallo  *\<app_naam >* aanduiding voor items met een unieke app-naam.</span><span class="sxs-lookup"><span data-stu-id="8511d-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="8511d-208">Deze naam wordt gebruikt als onderdeel van de standaard-URL Hallo Hallo voor Hallo web-app, zodat het Hallo-naam moet toobe uniek zijn in alle apps in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8511d-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="8511d-209">Wanneer het Hallo-web-app is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="8511d-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="8511d-210">Configureren van een omgevingsvariabele</span><span class="sxs-lookup"><span data-stu-id="8511d-210">Configure an environment variable</span></span>

<span data-ttu-id="8511d-211">Eerder in Hallo zelfstudie, u hardcoded Hallo databaseverbindingsreeks in _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="8511d-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="8511d-212">Aan de aanbevolen beveiligingsprocedure wilt u tookeep deze gevoelige gegevens buiten de Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="8511d-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="8511d-213">Voor uw app in Azure wordt uitgevoerd, gebruikt u een omgevingsvariabele in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="8511d-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="8511d-214">In App Service, stelt u omgevingsvariabelen als _appinstellingen_ met behulp van Hallo [az webapp config appsettings bijwerken](/cli/azure/webapp/config/appsettings#update) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8511d-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="8511d-215">Hallo volgende voorbeeld wordt een `MONGODB_URI` app-instelling in uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8511d-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="8511d-216">Vervang Hallo  *\<app_naam >*,  *\<cosmosdb_name >*, en  *\<primary_master_key >* tijdelijke aanduidingen.</span><span class="sxs-lookup"><span data-stu-id="8511d-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="8511d-217">In een Node.js-code, opent u deze app-instelling met `process.env.MONGODB_URI`, net zoals u toegang krijgen een omgevingsvariabele tot zou.</span><span class="sxs-lookup"><span data-stu-id="8511d-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="8511d-218">Nu uw too_config/env/production.js_ wijzigingen ongedaan Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8511d-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="8511d-219">Open _config/env/production.js_ opnieuw.</span><span class="sxs-lookup"><span data-stu-id="8511d-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="8511d-220">Houd er rekening mee dat Hallo standaard MEAN.js app is al geconfigureerde toouse Hallo `MONGODB_URI` omgevingsvariabele die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8511d-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="8511d-221">Lokale Git-implementatie configureren</span><span class="sxs-lookup"><span data-stu-id="8511d-221">Configure local git deployment</span></span> 

<span data-ttu-id="8511d-222">Gebruik Hallo [az webapp implementatiegebruiker ingesteld](/cli/azure/webapp/deployment/user#set) opdracht toocreate referenties voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="8511d-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="8511d-223">U kunt uw toepassing tooAzure App Service op verschillende manieren, met inbegrip van de FTP-, lokale Git, Visual Studio Team Services, GitHub en BitBucket implementeren.</span><span class="sxs-lookup"><span data-stu-id="8511d-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="8511d-224">Voor de FTP- en lokale Git, is het noodzakelijk toohave implementatie van een gebruiker geconfigureerd op Hallo server tooauthenticate uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="8511d-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="8511d-225">Deze gebruiker implementatie-account-niveau en verschilt van de account van uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8511d-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="8511d-226">U hoeft alleen tooconfigure deze implementatie gebruiker één keer.</span><span class="sxs-lookup"><span data-stu-id="8511d-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="8511d-227">Hallo opdracht, na Vervang in  *\<gebruikersnaam >* en  *\<wachtwoord >* met een nieuwe gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8511d-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="8511d-228">Hallo-gebruikersnaam moet uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="8511d-228">hello user name must be unique.</span></span> <span data-ttu-id="8511d-229">Hallo wachtwoord moet ten minste acht tekens lang zijn, met twee Hallo na drie elementen: letters, cijfers, symbolen.</span><span class="sxs-lookup"><span data-stu-id="8511d-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="8511d-230">Als u krijgt een ` 'Conflict'. Details: 409` fout, wijziging Hallo gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="8511d-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="8511d-231">Als er een ` 'Bad Request'. Details: 400`-fout optreedt, kiest u een sterker wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="8511d-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="8511d-232">Record Hallo-gebruikersnaam en wachtwoord voor gebruik in latere stappen wanneer u Hallo app implementeert.</span><span class="sxs-lookup"><span data-stu-id="8511d-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="8511d-233">Gebruik Hallo [bron in az webapp implementatie-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) opdracht tooconfigure lokale Git access toohello Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8511d-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="8511d-234">Wanneer Hallo implementatie gebruiker is geconfigureerd, wordt het hello Azure CLI Hallo implementatie URL voor uw Azure-web-app in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="8511d-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="8511d-235">De uitvoer van Hallo terminal Hallo kopiëren wordt dit gebruikt in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="8511d-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="8511d-236">TooAzure van Git push</span><span class="sxs-lookup"><span data-stu-id="8511d-236">Push tooAzure from Git</span></span>

<span data-ttu-id="8511d-237">Een Azure externe tooyour lokale Git-opslagplaats toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8511d-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="8511d-238">Push toohello Azure externe toodeploy uw Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8511d-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="8511d-239">U wordt gevraagd om Hallo wachtwoord die u eerder hebt opgegeven als onderdeel van Hallo maken van Hallo implementatie gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8511d-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="8511d-240">Azure App Service communiceert tijdens de implementatie van de voortgang met Git.</span><span class="sxs-lookup"><span data-stu-id="8511d-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="8511d-241">U merkt dat het implementatieproces hello wordt uitgevoerd [Gulp](http://gulpjs.com/) nadat `npm install`.</span><span class="sxs-lookup"><span data-stu-id="8511d-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="8511d-242">App Service Gulp of knorvis taken kan niet worden uitgevoerd tijdens de implementatie, zodat deze opslagplaats voorbeeld heeft twee extra bestanden in de hoofdmap directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="8511d-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="8511d-243">_.Deployment_ -dit bestand vertelt App Service-toorun `bash deploy.sh` als Hallo aangepaste implementatiescript.</span><span class="sxs-lookup"><span data-stu-id="8511d-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="8511d-244">_Deploy.sh_ -script voor aangepaste implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="8511d-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="8511d-245">Als u hello bestand bekijkt, ziet u dat deze wordt uitgevoerd `gulp prod` nadat `npm install` en `bower install`.</span><span class="sxs-lookup"><span data-stu-id="8511d-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="8511d-246">U kunt deze benadering tooadd elke stap tooyour implementatie op basis van Git gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8511d-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="8511d-247">Als u uw Azure-web-app op elk moment opnieuw opstart, wordt niet deze automatiseringstaken opnieuw uitvoeren App Service.</span><span class="sxs-lookup"><span data-stu-id="8511d-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="8511d-248">Toohello Azure-web-app bladeren</span><span class="sxs-lookup"><span data-stu-id="8511d-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="8511d-249">Bladeren toohello geïmplementeerd web-app met uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="8511d-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="8511d-250">Klik op **aanmelden** in Hallo bovenste menu en maak een dummy-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="8511d-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="8511d-251">Als u geslaagde en Hallo app automatisch aanmeldt heeft toohello gebruiker en vervolgens uw app MEAN.js gemaakt in Azure connectiviteit toohello MongoDB (Cosmos DB)-database.</span><span class="sxs-lookup"><span data-stu-id="8511d-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![MEAN.js-app uitgevoerd in Azure App Service](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="8511d-253">Selecteer **Admin > artikelen beheren** tooadd sommige artikelen.</span><span class="sxs-lookup"><span data-stu-id="8511d-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="8511d-254">**Gefeliciteerd!**</span><span class="sxs-lookup"><span data-stu-id="8511d-254">**Congratulations!**</span></span> <span data-ttu-id="8511d-255">U uitvoert een gegevensgestuurd Node.js-app in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8511d-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="8511d-256">Update-gegevensmodel en de implementatie opnieuw uit</span><span class="sxs-lookup"><span data-stu-id="8511d-256">Update data model and redeploy</span></span>

<span data-ttu-id="8511d-257">In deze stap maakt u Hallo wijzigen `article` data model en publiceren van uw tooAzure wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8511d-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="8511d-258">Hallo-gegevensmodel bijwerken</span><span class="sxs-lookup"><span data-stu-id="8511d-258">Update hello data model</span></span>

<span data-ttu-id="8511d-259">Open _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="8511d-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="8511d-260">In `ArticleSchema`, Voeg een `String` type aangeroepen `comment`.</span><span class="sxs-lookup"><span data-stu-id="8511d-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="8511d-261">Wanneer u bent klaar, ziet uw schema-code als volgt:</span><span class="sxs-lookup"><span data-stu-id="8511d-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="8511d-262">Hallo artikelen code bijwerken</span><span class="sxs-lookup"><span data-stu-id="8511d-262">Update hello articles code</span></span>

<span data-ttu-id="8511d-263">Bijwerken van Hallo rest van uw `articles` toouse code `comment`.</span><span class="sxs-lookup"><span data-stu-id="8511d-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="8511d-264">Er zijn vijf bestanden die u nodig hebt toomodify: Hallo server domeincontroller en Hallo vier client weergaven.</span><span class="sxs-lookup"><span data-stu-id="8511d-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="8511d-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="8511d-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="8511d-266">In Hallo `update` werkt, het toevoegen van een toewijzing voor `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="8511d-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="8511d-267">Hallo volgende code toont Hallo voltooid `update` functie:</span><span class="sxs-lookup"><span data-stu-id="8511d-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="8511d-268">Open _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="8511d-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="8511d-269">Hallo sluiten erboven `</section>` tag, het toevoegen van Hallo regel toodisplay na `comment` samen met de rest van de Hallo van Hallo artikelgegevens:</span><span class="sxs-lookup"><span data-stu-id="8511d-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="8511d-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="8511d-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="8511d-271">Hallo sluiten erboven `</a>` tag, het toevoegen van Hallo regel toodisplay na `comment` samen met de rest van de Hallo van Hallo artikelgegevens:</span><span class="sxs-lookup"><span data-stu-id="8511d-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="8511d-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="8511d-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="8511d-273">Hallo binnen `<div class="list-group">` element en erboven Hallo sluiten `</a>` tag, het toevoegen van Hallo regel toodisplay na `comment` samen met de rest van de Hallo van Hallo artikelgegevens:</span><span class="sxs-lookup"><span data-stu-id="8511d-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="8511d-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="8511d-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="8511d-275">Hallo zoeken `<div class="form-group">` element met de verzendknop hello, welke ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="8511d-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="8511d-276">Net boven deze tag toevoegen `<div class="form-group">` element waarmee mensen Hallo bewerken `comment` veld.</span><span class="sxs-lookup"><span data-stu-id="8511d-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="8511d-277">Uw nieuwe element moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="8511d-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="8511d-278">Uw wijzigingen lokaal testen</span><span class="sxs-lookup"><span data-stu-id="8511d-278">Test your changes locally</span></span>

<span data-ttu-id="8511d-279">Sla al uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="8511d-279">Save all your changes.</span></span>

<span data-ttu-id="8511d-280">Test uw wijzigingen opnieuw in de productiemodus.</span><span class="sxs-lookup"><span data-stu-id="8511d-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="8511d-281">Vergeet niet dat uw _config/env/production.js_ is hersteld en Hallo `MONGODB_URI` omgevingsvariabele wordt alleen ingesteld in uw Azure-web-app en niet op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8511d-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="8511d-282">Als u het configuratiebestand Hallo bekijkt, vindt u die Hallo productconfiguratie standaard toouse een lokale MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="8511d-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="8511d-283">Dit zorgt ervoor dat u productiegegevens niet raken als u uw codewijzigingen lokaal testen.</span><span class="sxs-lookup"><span data-stu-id="8511d-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="8511d-284">Navigeer te`http://localhost:8443` in een browser en zorg ervoor dat u bent aangemeld.</span><span class="sxs-lookup"><span data-stu-id="8511d-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="8511d-285">Selecteer **Admin > artikelen beheren**, klikt u vervolgens een artikel toevoegen door te selecteren van Hallo  **+**  knop.</span><span class="sxs-lookup"><span data-stu-id="8511d-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="8511d-286">U ziet Hallo nieuwe `Comment` textbox nu.</span><span class="sxs-lookup"><span data-stu-id="8511d-286">You see hello new `Comment` textbox now.</span></span>

![Toegevoegde opmerking veld tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="8511d-288">In terminal hello, stopt u Node.js door `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="8511d-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="8511d-289">TooAzure wijzigingen publiceren</span><span class="sxs-lookup"><span data-stu-id="8511d-289">Publish changes tooAzure</span></span>

<span data-ttu-id="8511d-290">Uw wijzigingen in Git en push ze Hallo code wijzigingen tooAzure.</span><span class="sxs-lookup"><span data-stu-id="8511d-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="8511d-291">Eenmaal Hallo `git push` is voltooid, gaat u tooyour Azure-web-app en de nieuwe functionaliteit Hallo uitproberen.</span><span class="sxs-lookup"><span data-stu-id="8511d-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![Model en de database wijzigingen tooAzure gepubliceerd](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="8511d-293">Als u alle artikelen die eerder is toegevoegd, kunt u nog steeds zien.</span><span class="sxs-lookup"><span data-stu-id="8511d-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="8511d-294">Bestaande gegevens in uw Cosmos-database is niet verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="8511d-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="8511d-295">Bovendien uw updates toohello gegevensschema en uw bestaande gegevens intact blijft.</span><span class="sxs-lookup"><span data-stu-id="8511d-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="8511d-296">Diagnostische logboeken</span><span class="sxs-lookup"><span data-stu-id="8511d-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="8511d-297">Als uw Node.js-toepassing in Azure App Service wordt uitgevoerd, kunt u Hallo console logboeken doorgesluisd tooyour terminal opvragen.</span><span class="sxs-lookup"><span data-stu-id="8511d-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="8511d-298">Op die manier kunt u Hallo dezelfde diagnostische ontvangt toohelp foutopsporing van toepassingsfouten.</span><span class="sxs-lookup"><span data-stu-id="8511d-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="8511d-299">toostart logboek streaming gebruik Hallo [az webapp logboek tail](/cli/azure/webapp/log#tail) opdracht.</span><span class="sxs-lookup"><span data-stu-id="8511d-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="8511d-300">Eenmaal streaming-logboek is gestart, worden uw Azure-web-app in Hallo browser tooget sommige webverkeer vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="8511d-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="8511d-301">U ziet nu de logboeken van console doorgesluisd tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="8511d-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="8511d-302">Stop log streaming op elk gewenst moment door typen `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="8511d-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="8511d-303">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="8511d-303">Manage your Azure web app</span></span>

<span data-ttu-id="8511d-304">Ga toohello [Azure-portal](https://portal.azure.com) toosee Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8511d-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="8511d-305">In het linkermenu hello, klikt u op **App Services**, klikt u op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="8511d-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="8511d-307">Standaard Hallo portal uw web-app toont **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="8511d-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="8511d-308">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="8511d-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="8511d-309">Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8511d-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="8511d-310">Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuratiepagina's die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="8511d-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="8511d-312">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8511d-312">Next steps</span></span>

<span data-ttu-id="8511d-313">Wat u hebt geleerd:</span><span class="sxs-lookup"><span data-stu-id="8511d-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8511d-314">Maak een MongoDB-database in Azure</span><span class="sxs-lookup"><span data-stu-id="8511d-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="8511d-315">Verbinding maken met een Node.js-app tooMongoDB</span><span class="sxs-lookup"><span data-stu-id="8511d-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="8511d-316">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="8511d-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="8511d-317">Hallo-gegevensmodel bijwerken en Hallo app implementeren</span><span class="sxs-lookup"><span data-stu-id="8511d-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="8511d-318">Logboeken van de stroom van Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="8511d-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="8511d-319">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="8511d-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="8511d-320">De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name tooyour web-app.</span><span class="sxs-lookup"><span data-stu-id="8511d-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="8511d-321">Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="8511d-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
