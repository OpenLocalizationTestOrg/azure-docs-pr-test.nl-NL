---
title: 'Azure Cosmos DB: Ontwikkelen met Hallo tabel API in .NET | Microsoft Docs'
description: Meer informatie over hoe toodevelop met tabel-API van Azure Cosmos DB met .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="d3909-103">Azure Cosmos DB: Ontwikkelen met Hallo tabel API in .NET</span><span class="sxs-lookup"><span data-stu-id="d3909-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="d3909-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d3909-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="d3909-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="d3909-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="d3909-106">Deze zelfstudie behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3909-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="d3909-107">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="d3909-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="d3909-108">Schakel de functionaliteit in Hallo app.config-bestand</span><span class="sxs-lookup"><span data-stu-id="d3909-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="d3909-109">Een tabel maken met de Hallo [tabel API](table-introduction.md) (preview)</span><span class="sxs-lookup"><span data-stu-id="d3909-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="d3909-110">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="d3909-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="d3909-111">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="d3909-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="d3909-112">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="d3909-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="d3909-113">Query-entiteiten met behulp van automatische secundaire indexen</span><span class="sxs-lookup"><span data-stu-id="d3909-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="d3909-114">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="d3909-114">Replace an entity</span></span> 
> * <span data-ttu-id="d3909-115">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="d3909-115">Delete an entity</span></span> 
> * <span data-ttu-id="d3909-116">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="d3909-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="d3909-117">Tabellen in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d3909-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="d3909-118">Azure Cosmos DB biedt Hallo [tabel API](table-introduction.md) (preview) voor toepassingen die een sleutel-waardearchief met een schema-less-ontwerp moeten.</span><span class="sxs-lookup"><span data-stu-id="d3909-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="d3909-119">[Azure Table storage](../storage/common/storage-introduction.md) SDK's en REST-API's kunnen worden gebruikt toowork met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d3909-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="d3909-120">U kunt Azure Cosmos DB toocreate tabellen met hoge doorvoer vereisten.</span><span class="sxs-lookup"><span data-stu-id="d3909-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="d3909-121">Azure Cosmos DB ondersteunt tabellen die zijn geoptimaliseerd voor doorvoer (ook wel eens premium-tabellen genoemd), en is momenteel beschikbaar in de openbare preview-versie.</span><span class="sxs-lookup"><span data-stu-id="d3909-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="d3909-122">Toouse Azure Table storage voor tabellen met hoge opslag en lagere doorvoer vereisten kan worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="d3909-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="d3909-123">Ondersteuning voor tabellen geoptimaliseerd voor opslag in een toekomstige update leidt tot Azure Cosmos DB en bestaande en nieuwe Azure Table storage-accounts naadloos worden bijgewerkt tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d3909-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="d3909-124">Als u momenteel Azure Table storage, krijgt u de volgende voordelen met preview-Hallo 'tabel premium' hello:</span><span class="sxs-lookup"><span data-stu-id="d3909-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="d3909-125">Directe [globale distributie](distribute-data-globally.md) met multihoming en [automatische en handmatige failover](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="d3909-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="d3909-126">Ondersteuning voor automatische schema-networkdirect indexeren tegen alle eigenschappen ('secundaire indexen') en snelle query 's</span><span class="sxs-lookup"><span data-stu-id="d3909-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="d3909-127">Ondersteuning voor [onafhankelijke schalen van opslag en doorvoer](partition-data.md), via verschillende regio's</span><span class="sxs-lookup"><span data-stu-id="d3909-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="d3909-128">Ondersteuning voor [toegewezen doorvoer per tabel](request-units.md) die kunnen worden geschaald van honderden toomillions van aanvragen per seconde</span><span class="sxs-lookup"><span data-stu-id="d3909-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="d3909-129">Ondersteuning voor [vijf instelbare consistentieniveaus](consistency-levels.md) tootrade beschikbaarheid, latentie en consistentiecontroles uit op basis van de behoeften van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="d3909-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="d3909-130">99,99% beschikbaarheid binnen één regio en de mogelijkheid tooadd meer regio's voor hogere beschikbaarheid en [toonaangevende uitgebreide serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db/) op algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="d3909-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="d3909-131">Werken met Hallo bestaande Azure-opslag .NET SDK en er geen code wijzigingen tooyour toepassing</span><span class="sxs-lookup"><span data-stu-id="d3909-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="d3909-132">Tijdens het Hallo-preview hello Azure Cosmos DB ondersteunt tabel-API met behulp van Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d3909-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="d3909-133">U kunt downloaden Hallo [Preview-SDK van Azure Storage](https://aka.ms/premiumtablenuget) vanuit NuGet, die Hallo is dezelfde klassen- en handtekeningen als Hallo [Azure-opslag-SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ook verbinding kan maken met tooAzure Cosmos DB accounts met Hallo Tabel-API.</span><span class="sxs-lookup"><span data-stu-id="d3909-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="d3909-134">toolearn meer informatie over complexe taken voor Azure Table-opslag, Zie:</span><span class="sxs-lookup"><span data-stu-id="d3909-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="d3909-135">Inleiding tooAzure Cosmos DB: tabel-API</span><span class="sxs-lookup"><span data-stu-id="d3909-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="d3909-136">Tabel-naslagdocumentatie voor meer informatie over beschikbare API's Hallo [Storage-clientbibliotheek voor .NET-verwijzing](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="d3909-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="d3909-137">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="d3909-137">About this tutorial</span></span>
<span data-ttu-id="d3909-138">Voor ontwikkelaars die bekend bent met hello Azure Table storage SDK en wilt toouse Hallo Premiumfuncties die beschikbaar is in deze zelfstudie met behulp van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d3909-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="d3909-139">Deze is gebaseerd op [aan de slag met Azure Table storage met .NET](table-storage-how-to-use-dotnet.md) en ziet u hoe tootake profiteren van extra mogelijkheden, zoals secundaire indexen, ingerichte doorvoer en multihoming.</span><span class="sxs-lookup"><span data-stu-id="d3909-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="d3909-140">We hebben betrekking op hoe toouse hello Azure portal toocreate een Cosmos-DB Azure-account, en vervolgens bouwen en implementeren van de toepassing van een tabel.</span><span class="sxs-lookup"><span data-stu-id="d3909-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="d3909-141">We helpt ook bij .NET-voorbeelden voor het maken en verwijderen van een tabel en invoegen, bijwerken, verwijderen en opvragen van tabelgegevens.</span><span class="sxs-lookup"><span data-stu-id="d3909-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="d3909-142">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken van Hallo **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d3909-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="d3909-143">Zorg ervoor dat u inschakelt **ontwikkelen van Azure** tijdens de installatie van Visual Studio Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3909-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="d3909-144">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="d3909-144">Create a database account</span></span>

<span data-ttu-id="d3909-145">Begint met het maken van een Azure DB die Cosmos-account in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="d3909-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="d3909-146">Hebt u al een Azure DB die Cosmos-account?</span><span class="sxs-lookup"><span data-stu-id="d3909-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="d3909-147">Als dit het geval is, gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d3909-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="d3909-148">Hebt u een Azure-DocumentDB-account?</span><span class="sxs-lookup"><span data-stu-id="d3909-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="d3909-149">Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d3909-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="d3909-150">Als u hello Azure Cosmos DB Emulator, volgt u stappen op Hallo [Azure Cosmos DB Emulator](local-emulator.md) toosetup Hallo emulator en gaat u verder te[instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="d3909-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="d3909-151">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="d3909-151">Clone hello sample application</span></span>

<span data-ttu-id="d3909-152">Nu gaan we een tabel-app vanuit github Hallo verbindingsreeks instellen en voer dit klonen.</span><span class="sxs-lookup"><span data-stu-id="d3909-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="d3909-153">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="d3909-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="d3909-154">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d3909-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="d3909-155">Open het oplossingsbestand Hallo in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3909-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="d3909-156">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="d3909-156">Update your connection string</span></span>

<span data-ttu-id="d3909-157">Nu gaat u terug toohello Azure portal tooget verbindingsreeksgegevens en kopieer dit naar Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="d3909-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="d3909-158">In Hallo [Azure-portal](http://portal.azure.com/), in uw Azure DB-Cosmos-account, klik op in de linkernavigatiebalk Hallo **sleutels**, en klik vervolgens op **lezen-schrijven sleutels**.</span><span class="sxs-lookup"><span data-stu-id="d3909-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="d3909-159">Gebruikt u de knoppen kopiëren Hallo aan de rechterkant Hallo van Hallo scherm toocopy Hallo-verbindingsreeks in Hallo app.config-bestand in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3909-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="d3909-160">Open in Visual Studio Hallo app.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="d3909-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="d3909-161">Kopieer de waarde van de URI van Hallo-portal (met behulp van de knop kopiëren Hallo), waardoor het Hallo Hallo account-sleutelwaarde in app.config. Hallo-accountnaam eerder hebt gemaakt voor account-name in app.config gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3909-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="d3909-162">toouse deze app met standaard Azure Table Storage, moet u toochange Hallo-verbindingsreeks in `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="d3909-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="d3909-163">Hallo-accountnaam gebruiken als tabel accountnaam en de sleutel als Azure Storage primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="d3909-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="d3909-164">Hallo-app bouwen en implementeren</span><span class="sxs-lookup"><span data-stu-id="d3909-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="d3909-165">In Visual Studio met de rechtermuisknop op Hallo-project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="d3909-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="d3909-166">In Hallo NuGet **Bladeren** in het vak ***WindowsAzure.Storage PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="d3909-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="d3909-167">Controleer **omvatten prerelease-versie**.</span><span class="sxs-lookup"><span data-stu-id="d3909-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="d3909-168">Installeren in Hallo resultaten Hallo **WindowsAzure.Storage PremiumTable** en kies Hallo preview-build `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="d3909-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="d3909-169">Deze actie installeert hello Azure Table storage pakket en alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d3909-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="d3909-170">Klik op CTRL + F5 toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3909-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="d3909-171">U kunt nu gaat u terug tooData Explorer en Zie query, wijzigen en werken met de gegevens van deze tabel.</span><span class="sxs-lookup"><span data-stu-id="d3909-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="d3909-172">toouse deze app met een Azure Cosmos DB Emulator, u zojuist hebt moet toochange Hallo-verbindingsreeks in `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="d3909-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="d3909-173">Hallo onder waarde voor de emulator gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3909-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="d3909-174">Mogelijkheden van Azure DB Cosmos</span><span class="sxs-lookup"><span data-stu-id="d3909-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="d3909-175">Azure Cosmos DB ondersteunt een aantal mogelijkheden die niet beschikbaar in hello Azure Table storage-API.</span><span class="sxs-lookup"><span data-stu-id="d3909-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="d3909-176">Hallo nieuwe functionaliteit kan worden ingeschakeld via de volgende Hallo `appSettings` configuratiewaarden.</span><span class="sxs-lookup"><span data-stu-id="d3909-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="d3909-177">Wij kon niet alle nieuwe handtekeningen overloads toohello voorbeeld of Azure-opslag-SDK introduceren.</span><span class="sxs-lookup"><span data-stu-id="d3909-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="d3909-178">Hiermee kunt u tooconnect tooboth standard en premium-tabellen en werken met andere Azure Storage-services zoals Blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="d3909-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="d3909-179">Sleutel</span><span class="sxs-lookup"><span data-stu-id="d3909-179">Key</span></span> | <span data-ttu-id="d3909-180">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d3909-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d3909-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="d3909-181">TableConnectionMode</span></span>  | <span data-ttu-id="d3909-182">Azure Cosmos DB ondersteunt twee modi voor connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="d3909-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="d3909-183">In `Gateway` modus aanvragen worden altijd gedaan toohello Azure DB die Cosmos-gateway het toohello bijbehorende gegevenspartities stuurt.</span><span class="sxs-lookup"><span data-stu-id="d3909-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="d3909-184">In `Direct` connectiviteitsmodus, Hallo client haalt Hallo toewijzing van tabellen toopartitions en aanvragen worden gedaan, rechtstreeks op basis van de gegevenspartities.</span><span class="sxs-lookup"><span data-stu-id="d3909-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="d3909-185">Het is raadzaam `Direct`, Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="d3909-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="d3909-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="d3909-186">TableConnectionProtocol</span></span> | <span data-ttu-id="d3909-187">Azure Cosmos DB ondersteunt twee verbindingsprotocollen - `Https` en `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="d3909-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="d3909-188">`Tcp`is de standaardinstelling Hallo en aanbevolen omdat het meer lightweight.</span><span class="sxs-lookup"><span data-stu-id="d3909-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="d3909-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="d3909-189">TablePreferredLocations</span></span> | <span data-ttu-id="d3909-190">Door komma's gescheiden lijst met aanbevolen (multihoming) locaties voor leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d3909-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="d3909-191">Elke Azure DB die Cosmos-account kan worden gekoppeld met 1-30 + regio's.</span><span class="sxs-lookup"><span data-stu-id="d3909-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="d3909-192">Elk clientexemplaar kunt u een subset van deze gebieden in volgorde van voorkeur Hallo voor lage latentie leesbewerkingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="d3909-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="d3909-193">Hallo-regio's moeten de namen van hun [weergavenamen](https://msdn.microsoft.com/library/azure/gg441293.aspx), bijvoorbeeld `West US`.</span><span class="sxs-lookup"><span data-stu-id="d3909-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="d3909-194">Zie ook [multihoming API's](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="d3909-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="d3909-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="d3909-195">TableConsistencyLevel</span></span> | <span data-ttu-id="d3909-196">U kunt uitschakelen handel tussen latentie, consistentie en beschikbaarheid door te kiezen tussen vijf goed gedefinieerde consistentieniveaus: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, en `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="d3909-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="d3909-197">Standaard is `Session`.</span><span class="sxs-lookup"><span data-stu-id="d3909-197">Default is `Session`.</span></span> <span data-ttu-id="d3909-198">Hallo keuze van de consistentieniveau maakt een belangrijke prestatieverbetering verschil in meerdere landen/regio-instellingen.</span><span class="sxs-lookup"><span data-stu-id="d3909-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="d3909-199">Zie [consistentieniveaus](consistency-levels.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3909-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="d3909-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="d3909-200">TableThroughput</span></span> | <span data-ttu-id="d3909-201">Gereserveerde doorvoer voor Hallo tabel uitgedrukt in aanvraageenheden (RU) per seconde.</span><span class="sxs-lookup"><span data-stu-id="d3909-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="d3909-202">Biedt ondersteuning voor één tabellen 100s-miljoenen RU/s.</span><span class="sxs-lookup"><span data-stu-id="d3909-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="d3909-203">Zie [Aanvraageenheden](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="d3909-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="d3909-204">Standaard is`400`</span><span class="sxs-lookup"><span data-stu-id="d3909-204">Default is `400`</span></span> |
| <span data-ttu-id="d3909-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="d3909-205">TableIndexingPolicy</span></span> | <span data-ttu-id="d3909-206">Consistente en automatische secundaire indexeren van alle kolommen in tabellen</span><span class="sxs-lookup"><span data-stu-id="d3909-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="d3909-207">JSON-tekenreeks die voldoen toohello beleidsspecificatie van het te indexeren.</span><span class="sxs-lookup"><span data-stu-id="d3909-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="d3909-208">Zie [indexeren beleid](indexing-policies.md) toosee hoe u indexering beleid tooinclude en uitsluiten specifieke kolommen kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d3909-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="d3909-209">Automatische indexering van alle eigenschappen (hash voor tekenreeksen) en bereik voor getallen</span><span class="sxs-lookup"><span data-stu-id="d3909-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="d3909-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="d3909-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="d3909-211">Maximum aantal items geretourneerd per tabelquery in een enkel retour Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="d3909-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="d3909-212">Standaard is `-1`, waarmee Azure Cosmos DB dynamisch bepalen Hallo waarde tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="d3909-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="d3909-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="d3909-213">TableQueryEnableScan</span></span> | <span data-ttu-id="d3909-214">Als Hallo query niet kan Hallo index voor elk filter, voer het toch via een scan.</span><span class="sxs-lookup"><span data-stu-id="d3909-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="d3909-215">Standaard is `false`.</span><span class="sxs-lookup"><span data-stu-id="d3909-215">Default is `false`.</span></span>|
| <span data-ttu-id="d3909-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="d3909-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="d3909-217">Hallo mate van parallelle uitvoering voor uitvoering van een query cross-partitie.</span><span class="sxs-lookup"><span data-stu-id="d3909-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="d3909-218">`0`seriële met geen vooraf ophalen, is `1` serieel met vooraf ophalen en hogere waarden toename Hallo frequentie van parallelle uitvoering.</span><span class="sxs-lookup"><span data-stu-id="d3909-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="d3909-219">Standaard is `-1`, waarmee Azure Cosmos DB dynamisch bepalen Hallo waarde tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="d3909-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="d3909-220">toochange Hallo-standaardwaarde, open Hallo `app.config` bestand vanuit Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3909-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="d3909-221">Hallo-inhoud van Hallo toevoegen `<appSettings>` element hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d3909-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="d3909-222">Vervang `account-name` met Hallo-naam van uw opslagaccount en `account-key` door de toegangssleutel voor uw account.</span><span class="sxs-lookup"><span data-stu-id="d3909-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="d3909-223">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="d3909-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="d3909-224">Open Hallo `Program.cs` bestands- en u vindt dat deze regels code Hallo tabel resources maken.</span><span class="sxs-lookup"><span data-stu-id="d3909-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="d3909-225">Hallo tabel client maken</span><span class="sxs-lookup"><span data-stu-id="d3909-225">Create hello table client</span></span>
<span data-ttu-id="d3909-226">U initialiseren een `CloudTableClient` tooconnect toohello tabel account.</span><span class="sxs-lookup"><span data-stu-id="d3909-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="d3909-227">Deze client is geïnitialiseerd met behulp van Hallo `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, en `TablePreferredLocations` configuratiewaarden als opgegeven in de instellingen van de Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="d3909-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="d3909-228">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="d3909-228">Create a table</span></span>
<span data-ttu-id="d3909-229">Maakt u een tabel met `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="d3909-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="d3909-230">Tabellen in Azure Cosmos DB onafhankelijk kunnen schalen in termen van opslag en de doorvoer en automatisch partitioneren is verwerkt door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="d3909-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="d3909-231">Azure Cosmos DB ondersteunt zowel vaste grootte als onbeperkt aantal tabellen.</span><span class="sxs-lookup"><span data-stu-id="d3909-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="d3909-232">Zie [partitioneren in Azure Cosmos DB](partition-data.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d3909-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="d3909-233">Er is een belangrijk verschil in hoe tabellen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3909-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="d3909-234">Azure Cosmos DB reserveert doorvoer, in tegenstelling tot Azure storage op basis van verbruik model voor transacties.</span><span class="sxs-lookup"><span data-stu-id="d3909-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="d3909-235">Hallo-reservering model biedt twee belangrijke voordelen:</span><span class="sxs-lookup"><span data-stu-id="d3909-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="d3909-236">De doorvoer is toegewezen/gereserveerd, zodat u nooit kunnen beperkt ophalen als uw aanvraagsnelheid op of onder uw ingerichte doorvoer is</span><span class="sxs-lookup"><span data-stu-id="d3909-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="d3909-237">Hallo-reservering model is meer [rendabel voor doorvoer zware workloads](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="d3909-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="d3909-238">U kunt Hallo standaard doorvoer configureren door het Hallo-instelling voor `TableThroughput` in termen van RU (aanvraageenheden) per seconde.</span><span class="sxs-lookup"><span data-stu-id="d3909-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="d3909-239">Het lezen van een entiteit 1 KB is genormaliseerd als 1 RU en andere bewerkingen zijn genormaliseerde tooa vaste RU-waarde op basis van hun verbruik CPU, geheugen en IOPS.</span><span class="sxs-lookup"><span data-stu-id="d3909-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="d3909-240">Meer informatie over [Aanvraageenheden in Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="d3909-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d3909-241">Terwijl de SDK-tabelopslag biedt momenteel geen ondersteuning voor doorvoer wijzigen, kunt u Hallo doorvoer onmiddellijk op elk gewenst moment hello Azure-portal of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d3909-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="d3909-242">Vervolgens we doorlopen Hallo eenvoudige lezen en schrijven (CRUD)-bewerkingen met hello Azure Table storage SDK.</span><span class="sxs-lookup"><span data-stu-id="d3909-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="d3909-243">Deze zelfstudie wordt gedemonstreerd voorspelbare lage één cijfer milliseconde latenties en snelle query's die worden geleverd door Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d3909-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="d3909-244">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="d3909-244">Add an entity tooa table</span></span>
<span data-ttu-id="d3909-245">Entiteiten in de Azure-tabelopslag van Hallo uitbreiden `TableEntity` klasse en moet `PartitionKey` en `RowKey` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="d3909-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="d3909-246">Hier volgt een voorbeeld-definitie voor een klantentiteit.</span><span class="sxs-lookup"><span data-stu-id="d3909-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="d3909-247">Hallo volgende fragment toont hoe tooinsert een entiteit met Azure storage SDK Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3909-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="d3909-248">Azure Cosmos DB is ontworpen voor lage latentie op elke schaal gegarandeerd via Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="d3909-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="d3909-249">Schrijfbewerkingen voltooien < 15 ms op p99 en ~ 6 ms op p50 voor toepassingen die worden uitgevoerd dezelfde regio bevinden als hello Azure Cosmos DB account Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3909-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="d3909-250">En deze duur accounts voor Hallo fact die schrijft back toohello client zijn bevestigd nadat ze zijn synchroon gerepliceerd, blijvend doorgevoerd, en alle inhoud wordt geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="d3909-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="d3909-251">Hallo tabel-API voor Azure DB die Cosmos is een Preview-versie.</span><span class="sxs-lookup"><span data-stu-id="d3909-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="d3909-252">Algemene beschikbaarheid worden Hallo p99 latentie garanties ondersteund door serviceovereenkomsten net als andere Azure Cosmos DB-API's.</span><span class="sxs-lookup"><span data-stu-id="d3909-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="d3909-253">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="d3909-253">Insert a batch of entities</span></span>
<span data-ttu-id="d3909-254">Azure Table storage ondersteunt een bewerking API van batch, waarmee u updates, verwijderingen, combineren en voegt in dezelfde batchbewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3909-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="d3909-255">Azure Cosmos DB heeft geen enkele van Hallo beperkingen op Hallo batch-API als Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="d3909-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="d3909-256">Bijvoorbeeld, kunt u meerdere leesbewerkingen binnen een batch uitvoeren, kunt u meerdere schrijfbewerkingen toohello uitvoeren dezelfde entiteit binnen een batch en er is geen limiet van 100 bewerkingen per batch.</span><span class="sxs-lookup"><span data-stu-id="d3909-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="d3909-257">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="d3909-257">Retrieve a single entity</span></span>
<span data-ttu-id="d3909-258">(Opgehaald) opgehaald in Azure Cosmos DB voltooid < 10 ms op p99 en ~ 1 ms op p50 in Hallo dezelfde Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="d3909-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="d3909-259">Zo veel gebieden tooyour account toevoegen voor leesbewerkingen lage latentie en implementeren van toepassingen tooread van hun lokale regio ('multihomed') door in te stellen `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="d3909-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="d3909-260">U kunt met behulp van de volgende codefragment Hallo één entiteit ophalen:</span><span class="sxs-lookup"><span data-stu-id="d3909-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="d3909-261">Meer informatie over multihoming API's op [ontwikkelen met meerdere regio's](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="d3909-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="d3909-262">Query-entiteiten met behulp van automatische secundaire indexen</span><span class="sxs-lookup"><span data-stu-id="d3909-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="d3909-263">Tabellen kunnen worden opgevraagd met Hallo `TableQuery` klasse.</span><span class="sxs-lookup"><span data-stu-id="d3909-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="d3909-264">Azure Cosmos-database heeft een schrijven geoptimaliseerd database-engine die automatisch alle kolommen in de tabel indexeert.</span><span class="sxs-lookup"><span data-stu-id="d3909-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="d3909-265">Indexeren in Azure DB die Cosmos is agnostisch tooschema.</span><span class="sxs-lookup"><span data-stu-id="d3909-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="d3909-266">Dus wordt zelfs als uw schema afwijkt van rijen, of als Hallo schema gedurende een bepaalde periode zich verder ontwikkelen, deze automatisch geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="d3909-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="d3909-267">Omdat Azure Cosmos DB automatische secundaire indexen ondersteunt, wordt een query uitgevoerd naar een eigenschap Hallo index kunnen gebruiken en efficiënt worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="d3909-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="d3909-268">In voorbeeld van Azure DB die Cosmos Hallo ondersteunt dezelfde functionaliteit als Azure Table-opslag voor Hallo API van de tabel zoeken.</span><span class="sxs-lookup"><span data-stu-id="d3909-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="d3909-269">Azure Cosmos DB biedt ook ondersteuning voor sorteren, statistische functies, georuimtelijke query hiërarchie en een groot aantal ingebouwde functies.</span><span class="sxs-lookup"><span data-stu-id="d3909-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="d3909-270">Hallo aanvullende functionaliteit worden vermeld in de tabel API Hallo in een toekomstige service-update.</span><span class="sxs-lookup"><span data-stu-id="d3909-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="d3909-271">Zie [Azure Cosmos DB-query](documentdb-sql-query.md) voor een overzicht van deze mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d3909-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="d3909-272">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="d3909-272">Replace an entity</span></span>
<span data-ttu-id="d3909-273">tooupdate een entiteit ophalen uit de tabelservice hello, Hallo entiteitsobject wijzigen en vervolgens weer toohello tabelservice Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="d3909-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="d3909-274">Hallo wijzigt volgende code het telefoonnummer van een bestaande klant.</span><span class="sxs-lookup"><span data-stu-id="d3909-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="d3909-275">Op deze manier kunt u uitvoeren `InsertOrMerge` of `Merge` bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d3909-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="d3909-276">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="d3909-276">Delete an entity</span></span>
<span data-ttu-id="d3909-277">U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald met behulp van Hallo hetzelfde patroon weergegeven voor het bijwerken van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="d3909-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="d3909-278">Hallo na de code opgehaald en wordt een klantentiteit verwijderd.</span><span class="sxs-lookup"><span data-stu-id="d3909-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="d3909-279">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="d3909-279">Delete a table</span></span>
<span data-ttu-id="d3909-280">Ten slotte verwijdert Hallo volgende codevoorbeeld een tabel uit een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d3909-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="d3909-281">U kunt verwijderen en opnieuw maken van een tabel met Azure Cosmos DB onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="d3909-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="d3909-282">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="d3909-282">Clean up resources</span></span> 

<span data-ttu-id="d3909-283">Als u deze app niet toocontinue toouse gaat, gebruikt u Hallo stappen toodelete alle resources die zijn gemaakt met deze zelfstudie in hello Azure-portal te volgen.</span><span class="sxs-lookup"><span data-stu-id="d3909-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="d3909-284">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d3909-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="d3909-285">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="d3909-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d3909-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3909-286">Next steps</span></span>

<span data-ttu-id="d3909-287">In deze zelfstudie wordt besproken hoe tooget gestart met behulp van Azure DB die Cosmos Hello tabel API en u Hallo volgende hebt gedaan:</span><span class="sxs-lookup"><span data-stu-id="d3909-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="d3909-288">Een Azure DB die Cosmos-account gemaakt</span><span class="sxs-lookup"><span data-stu-id="d3909-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="d3909-289">Ingeschakelde functionaliteit in Hallo app.config-bestand</span><span class="sxs-lookup"><span data-stu-id="d3909-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="d3909-290">Een tabel gemaakt</span><span class="sxs-lookup"><span data-stu-id="d3909-290">Created a table</span></span> 
> * <span data-ttu-id="d3909-291">Een entiteit tooa tabel toegevoegd</span><span class="sxs-lookup"><span data-stu-id="d3909-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="d3909-292">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="d3909-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="d3909-293">Één entiteit opgehaald</span><span class="sxs-lookup"><span data-stu-id="d3909-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="d3909-294">De query entiteiten met behulp van automatische secundaire indexen</span><span class="sxs-lookup"><span data-stu-id="d3909-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="d3909-295">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="d3909-295">Replaced an entity</span></span> 
> * <span data-ttu-id="d3909-296">Een entiteit wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="d3909-296">Deleted an entity</span></span> 
> * <span data-ttu-id="d3909-297">Een tabel verwijderd</span><span class="sxs-lookup"><span data-stu-id="d3909-297">Deleted a table</span></span>  

<span data-ttu-id="d3909-298">U kunt nu de volgende zelfstudie toohello gaan en meer informatie over het opvragen van tabelgegevens.</span><span class="sxs-lookup"><span data-stu-id="d3909-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d3909-299">Query's uitvoeren met Hallo tabel-API</span><span class="sxs-lookup"><span data-stu-id="d3909-299">Query with hello Table API</span></span>](tutorial-query-table.md)
