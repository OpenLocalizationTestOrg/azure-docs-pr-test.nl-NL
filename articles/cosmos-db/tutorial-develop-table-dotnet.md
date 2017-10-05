---
title: 'Azure Cosmos DB: Ontwikkelen met de tabel API in .NET | Microsoft Docs'
description: Meer informatie over het ontwikkelen met Azure Cosmos DB tabel API met .NET
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
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="8c5d9-103">Azure Cosmos DB: Ontwikkelen met de tabel API in .NET</span><span class="sxs-lookup"><span data-stu-id="8c5d9-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="8c5d9-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="8c5d9-105">U kunt snel databases maken van documenten, sleutel/waarde-paren en grafen en hier query’s op uitvoeren. Deze databases genieten allemaal het voordeel van de wereldwijde distributie en horizontale schaalmogelijkheden die ten grondslag liggen aan Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="8c5d9-106">Deze zelfstudie bevat de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="8c5d9-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="8c5d9-107">Maak een Azure Cosmos DB-account</span><span class="sxs-lookup"><span data-stu-id="8c5d9-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="8c5d9-108">Schakel in het bestand app.config-functionaliteit</span><span class="sxs-lookup"><span data-stu-id="8c5d9-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="8c5d9-109">Maak een tabel met de [tabel API](table-introduction.md) (preview)</span><span class="sxs-lookup"><span data-stu-id="8c5d9-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="8c5d9-110">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="8c5d9-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="8c5d9-111">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="8c5d9-112">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="8c5d9-113">Query-entiteiten met behulp van automatische secundaire indexen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="8c5d9-114">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-114">Replace an entity</span></span> 
> * <span data-ttu-id="8c5d9-115">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-115">Delete an entity</span></span> 
> * <span data-ttu-id="8c5d9-116">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="8c5d9-117">Tabellen in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8c5d9-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="8c5d9-118">Azure Cosmos DB biedt de [tabel API](table-introduction.md) (preview) voor toepassingen die een sleutel-waardearchief met een schema-less-ontwerp moeten.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="8c5d9-119">[Azure-tabelopslag](../storage/common/storage-introduction.md) SDK‘s en REST-API‘s kunnen worden gebruikt om te werken met Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="8c5d9-120">U kunt Azure Cosmos DB gebruiken om tabellen te maken met hoge vereisten voor doorvoersnelheid.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="8c5d9-121">Azure Cosmos DB ondersteunt tabellen die zijn geoptimaliseerd voor doorvoer (ook wel eens premium-tabellen genoemd), en is momenteel beschikbaar in de openbare preview-versie.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="8c5d9-122">U kunt Azure-tabelopslag blijven gebruiken voor tabellen met hoge vereisten voor opslag en lagere vereisten voor doorvoer.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="8c5d9-123">Ondersteuning voor tabellen geoptimaliseerd voor opslag in een toekomstige update leidt tot Azure Cosmos DB en bestaande en nieuwe Azure Table storage-accounts wordt probleemloos bijgewerkt naar Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="8c5d9-124">Als u momenteel Azure Table storage, krijgt u de volgende voordelen met de preview 'tabel premium':</span><span class="sxs-lookup"><span data-stu-id="8c5d9-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="8c5d9-125">Directe [globale distributie](distribute-data-globally.md) met multihoming en [automatische en handmatige failover](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="8c5d9-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="8c5d9-126">Ondersteuning voor automatische schema-networkdirect indexeren tegen alle eigenschappen ('secundaire indexen') en snelle query 's</span><span class="sxs-lookup"><span data-stu-id="8c5d9-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="8c5d9-127">Ondersteuning voor [onafhankelijke schalen van opslag en doorvoer](partition-data.md), via verschillende regio's</span><span class="sxs-lookup"><span data-stu-id="8c5d9-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="8c5d9-128">Ondersteuning voor [toegewezen doorvoer per tabel](request-units.md) die kunnen worden geschaald van honderden miljoenen aanvragen per seconde</span><span class="sxs-lookup"><span data-stu-id="8c5d9-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="8c5d9-129">Ondersteuning voor [vijf instelbare consistentieniveaus](consistency-levels.md) moeten op de handel uitschakelen beschikbaarheid, latentie en consistentie op basis van uw toepassing</span><span class="sxs-lookup"><span data-stu-id="8c5d9-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="8c5d9-130">99,99% beschikbaarheid binnen één regio, en het toevoegen van meer regio's voor hogere beschikbaarheid en [toonaangevende uitgebreide serviceovereenkomsten](https://azure.microsoft.com/support/legal/sla/cosmos-db/) op algemene beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="8c5d9-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="8c5d9-131">Werken met de bestaande Azure-opslag .NET SDK en geen codewijzigingen in uw toepassing</span><span class="sxs-lookup"><span data-stu-id="8c5d9-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="8c5d9-132">Tijdens de preview ondersteunt Azure Cosmos DB de API van de tabel met de .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="8c5d9-133">U kunt downloaden de [Preview-SDK van Azure Storage](https://aka.ms/premiumtablenuget) van NuGet, die dezelfde klassen en handtekeningen als heeft de [Azure-opslag-SDK](https://www.nuget.org/packages/WindowsAzure.Storage), maar ook verbinding kunt maken met Azure DB die Cosmos-accounts met behulp van de tabel-API.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="8c5d9-134">Zie voor meer informatie over complexe Azure Table storage taken:</span><span class="sxs-lookup"><span data-stu-id="8c5d9-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="8c5d9-135">Inleiding tot Azure Cosmos DB: tabel API</span><span class="sxs-lookup"><span data-stu-id="8c5d9-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="8c5d9-136">De tabel-naslagdocumentatie voor meer informatie over beschikbare API's [Storage-clientbibliotheek voor .NET-verwijzing](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="8c5d9-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="8c5d9-137">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="8c5d9-137">About this tutorial</span></span>
<span data-ttu-id="8c5d9-138">Voor ontwikkelaars die bekend bent met het Azure Table-opslag-SDK en wilt gebruiken, de premiumfuncties die beschikbaar is in deze zelfstudie met behulp van Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="8c5d9-139">Deze is gebaseerd op [aan de slag met Azure Table storage met .NET](table-storage-how-to-use-dotnet.md) en laat zien hoe om te profiteren van extra mogelijkheden, zoals secundaire indexen, ingerichte doorvoer en multihoming.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="8c5d9-140">We uitgelegd hoe de Azure portal gebruiken voor een Azure DB die Cosmos-account maken en bouwen en implementeren van de toepassing van een tabel.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="8c5d9-141">We helpt ook bij .NET-voorbeelden voor het maken en verwijderen van een tabel en invoegen, bijwerken, verwijderen en opvragen van tabelgegevens.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="8c5d9-142">Als u Visual Studio 2017 geïnstalleerd nog geen hebt, kunt u downloaden en gebruiken de **gratis** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="8c5d9-143">Zorg ervoor dat u **Azure-ontwikkeling** inschakelt tijdens de installatie van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="8c5d9-144">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="8c5d9-144">Create a database account</span></span>

<span data-ttu-id="8c5d9-145">Begint met het maken van een Azure DB die Cosmos-account in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="8c5d9-146">Hebt u al een Azure DB die Cosmos-account?</span><span class="sxs-lookup"><span data-stu-id="8c5d9-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="8c5d9-147">Als dit het geval is, gaat u verder met [instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="8c5d9-148">Hebt u een Azure-DocumentDB-account?</span><span class="sxs-lookup"><span data-stu-id="8c5d9-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="8c5d9-149">Als u dus uw account is nu een Cosmos-DB Azure-account en kunt u verder gaan naar [instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="8c5d9-150">Als u de Emulator Azure Cosmos DB, volgt u de stappen in [Azure Cosmos DB Emulator](local-emulator.md) instellen van de emulator en gaat u verder met [instellen van uw Visual Studio-oplossing](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="8c5d9-151">De voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-151">Clone the sample application</span></span>

<span data-ttu-id="8c5d9-152">We gaan nu een Table-app klonen vanaf GitHub, de verbindingsreeks instellen en de app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="8c5d9-153">Open een git-terminalvenster zoals git bash en `cd` naar een werkmap.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="8c5d9-154">Voer de volgende opdracht uit om de voorbeeldopslagplaats te klonen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="8c5d9-155">Open vervolgens het oplossingenbestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="8c5d9-156">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="8c5d9-156">Update your connection string</span></span>

<span data-ttu-id="8c5d9-157">Ga nu terug naar Azure Portal om de verbindingsreeksinformatie op te halen en kopieer deze in de app.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="8c5d9-158">Klik in [Azure Portal](http://portal.azure.com/), in uw Azure Cosmos DB-account, in het linker navigatiegedeelte op **Sleutels** en klik vervolgens op **Sleutels voor lezen/schrijven**.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="8c5d9-159">U gebruikt de knoppen kopiëren aan de rechterkant van het scherm voor het kopiëren van de verbindingsreeks naar het bestand app.config in de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="8c5d9-160">In Visual Studio opent u het bestand app.config.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="8c5d9-161">Uw URI-waarde kopiëren vanuit de portal (met behulp van de knop kopiëren) en maakt u de waarde van de accountsleutel in app.config. Gebruik de accountnaam voor accountnaam in app.config eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="8c5d9-162">Om deze app met standaard Azure Table Storage gebruiken, moet u de verbindingsreeks in wijzigen `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="8c5d9-163">De accountnaam gebruiken als tabel accountnaam en de sleutel als Azure Storage primaire sleutel.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="8c5d9-164">De app bouwen en implementeren</span><span class="sxs-lookup"><span data-stu-id="8c5d9-164">Build and deploy the app</span></span>
1. <span data-ttu-id="8c5d9-165">Klik in Visual Studio met de rechtermuisknop op het project in **Solution Explorer** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="8c5d9-166">Typ in het vak **Bladeren** in NuGet ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="8c5d9-167">Controleer **omvatten prerelease-versie**.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="8c5d9-168">Installeren van de resultaten de **WindowsAzure.Storage PremiumTable** en kies de preview-build `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="8c5d9-169">Deze actie installeert het Azure Table storage-pakket en alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="8c5d9-170">Klik op CTRL+F5 om de toepassing te starten.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="8c5d9-171">U kunt nu gaat u terug naar de Data Explorer en Zie query, wijzigen en werken met de gegevens van deze tabel.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="8c5d9-172">Voor het gebruik van deze app met een Azure-Emulator Cosmos DB, hoeft u alleen te wijzigen van de verbindingsreeks in `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="8c5d9-173">Gebruik de onderstaande waarde voor de emulator.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="8c5d9-174">Mogelijkheden van Azure DB Cosmos</span><span class="sxs-lookup"><span data-stu-id="8c5d9-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="8c5d9-175">Azure Cosmos DB ondersteunt een aantal mogelijkheden die niet beschikbaar in de Azure Table storage-API.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="8c5d9-176">De nieuwe functionaliteit kan worden ingeschakeld via de volgende `appSettings` configuratiewaarden.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="8c5d9-177">Wij kon niet alle nieuwe handtekeningen of overloads voor de preview-opslag-SDK van Azure introduceren.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="8c5d9-178">Hiermee kunt u verbinding maken met de standard en premium-tabellen en werken met andere Azure Storage-services zoals Blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="8c5d9-179">Sleutel</span><span class="sxs-lookup"><span data-stu-id="8c5d9-179">Key</span></span> | <span data-ttu-id="8c5d9-180">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8c5d9-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c5d9-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="8c5d9-181">TableConnectionMode</span></span>  | <span data-ttu-id="8c5d9-182">Azure Cosmos DB ondersteunt twee modi voor connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="8c5d9-183">In `Gateway` modus aanvragen worden altijd aangebracht in de Azure DB die Cosmos-gateway stuurt deze door naar de bijbehorende gegevenspartities.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="8c5d9-184">In `Direct` connectiviteitsmodus, de client haalt de toewijzing van tabellen partities en aanvragen worden gedaan, rechtstreeks op basis van de gegevenspartities.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="8c5d9-185">Het is raadzaam `Direct`, de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="8c5d9-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="8c5d9-186">TableConnectionProtocol</span></span> | <span data-ttu-id="8c5d9-187">Azure Cosmos DB ondersteunt twee verbindingsprotocollen - `Https` en `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="8c5d9-188">`Tcp`de standaardwaarde is en omdat het meer lightweight aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="8c5d9-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="8c5d9-189">TablePreferredLocations</span></span> | <span data-ttu-id="8c5d9-190">Door komma's gescheiden lijst met aanbevolen (multihoming) locaties voor leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="8c5d9-191">Elke Azure DB die Cosmos-account kan worden gekoppeld met 1-30 + regio's.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="8c5d9-192">Elk clientexemplaar kunt u een subset van deze gebieden in de gewenste volgorde voor lage latentie leesbewerkingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="8c5d9-193">De regio's moeten de namen van hun [weergavenamen](https://msdn.microsoft.com/library/azure/gg441293.aspx), bijvoorbeeld `West US`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="8c5d9-194">Zie ook [multihoming API's](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="8c5d9-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="8c5d9-195">TableConsistencyLevel</span></span> | <span data-ttu-id="8c5d9-196">U kunt uitschakelen handel tussen latentie, consistentie en beschikbaarheid door te kiezen tussen vijf goed gedefinieerde consistentieniveaus: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, en `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="8c5d9-197">Standaard is `Session`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-197">Default is `Session`.</span></span> <span data-ttu-id="8c5d9-198">De keuze van de consistentieniveau maakt een belangrijke prestatieverbetering verschil in meerdere landen/regio-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="8c5d9-199">Zie [consistentieniveaus](consistency-levels.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="8c5d9-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="8c5d9-200">TableThroughput</span></span> | <span data-ttu-id="8c5d9-201">Gereserveerde doorvoer voor de tabel die is uitgedrukt in aanvraageenheden (RU) per seconde.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="8c5d9-202">Biedt ondersteuning voor één tabellen 100s-miljoenen RU/s.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="8c5d9-203">Zie [Aanvraageenheden](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="8c5d9-204">Standaard is`400`</span><span class="sxs-lookup"><span data-stu-id="8c5d9-204">Default is `400`</span></span> |
| <span data-ttu-id="8c5d9-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="8c5d9-205">TableIndexingPolicy</span></span> | <span data-ttu-id="8c5d9-206">Consistente en automatische secundaire indexeren van alle kolommen in tabellen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="8c5d9-207">JSON-tekenreeks is die voldoet aan de beleidsspecificatie voor indexering.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="8c5d9-208">Zie [indexeren beleid](indexing-policies.md) om te zien hoe u indexeringsbeleid als u wilt opnemen en uitsluiten van specifieke kolommen kunt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="8c5d9-209">Automatische indexering van alle eigenschappen (hash voor tekenreeksen) en bereik voor getallen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="8c5d9-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="8c5d9-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="8c5d9-211">Het maximum aantal items geretourneerd per tabelquery in een enkel retour configureren.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="8c5d9-212">Standaard is `-1`, waarmee Azure Cosmos DB dynamisch bepalen van de waarde tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="8c5d9-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="8c5d9-213">TableQueryEnableScan</span></span> | <span data-ttu-id="8c5d9-214">Als de query niet kan de index voor elk filter, klikt u vervolgens het toch uitvoeren via een scan.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="8c5d9-215">Standaard is `false`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-215">Default is `false`.</span></span>|
| <span data-ttu-id="8c5d9-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="8c5d9-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="8c5d9-217">De mate van parallelle uitvoering voor uitvoering van een query cross-partitie.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="8c5d9-218">`0`seriële met geen vooraf ophalen, is `1` is seriële met waarden vooraf ophalen en hoger de snelheid van parallelle uitvoering verhogen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="8c5d9-219">Standaard is `-1`, waarmee Azure Cosmos DB dynamisch bepalen van de waarde tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="8c5d9-220">De standaardwaarde wilt wijzigen, opent u de `app.config` bestand vanuit Solution Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="8c5d9-221">Voeg de inhoud van het element `<appSettings>` hieronder toe.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="8c5d9-222">Vervang `account-name` met de naam van uw opslagaccount en `account-key` door de toegangssleutel voor uw account.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="8c5d9-223">Laten we eens kijken wat er precies gebeurt in de app.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="8c5d9-224">Open de `Program.cs` bestands- en u dat deze regels code maken met de resources van de tabel zoeken.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="8c5d9-225">De tabel-client maken</span><span class="sxs-lookup"><span data-stu-id="8c5d9-225">Create the table client</span></span>
<span data-ttu-id="8c5d9-226">U initialiseren een `CloudTableClient` verbinding maken met het account van de tabel.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="8c5d9-227">Deze client is geïnitialiseerd met behulp van de `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, en `TablePreferredLocations` configuratiewaarden als opgegeven in de app-instellingen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="8c5d9-228">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="8c5d9-228">Create a table</span></span>
<span data-ttu-id="8c5d9-229">Maakt u een tabel met `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="8c5d9-230">Tabellen in Azure Cosmos DB onafhankelijk kunnen schalen in termen van opslag en de doorvoer en automatisch partitioneren is verwerkt door de service.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="8c5d9-231">Azure Cosmos DB ondersteunt zowel vaste grootte als onbeperkt aantal tabellen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="8c5d9-232">Zie [partitioneren in Azure Cosmos DB](partition-data.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="8c5d9-233">Er is een belangrijk verschil in hoe tabellen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="8c5d9-234">Azure Cosmos DB reserveert doorvoer, in tegenstelling tot Azure storage op basis van verbruik model voor transacties.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="8c5d9-235">Het model reservering heeft twee belangrijke voordelen:</span><span class="sxs-lookup"><span data-stu-id="8c5d9-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="8c5d9-236">De doorvoer is toegewezen/gereserveerd, zodat u nooit kunnen beperkt ophalen als uw aanvraagsnelheid op of onder uw ingerichte doorvoer is</span><span class="sxs-lookup"><span data-stu-id="8c5d9-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="8c5d9-237">Het model reservering is meer [rendabel voor doorvoer zware workloads](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="8c5d9-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="8c5d9-238">U kunt de standaard-doorvoer configureren met het configureren van de instelling voor `TableThroughput` in termen van RU (aanvraageenheden) per seconde.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="8c5d9-239">Het lezen van een entiteit 1 KB is genormaliseerd als 1 RU en andere bewerkingen zijn genormaliseerd op een vaste RU-waarde op basis van hun verbruik CPU, geheugen en IOPS.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="8c5d9-240">Meer informatie over [Aanvraageenheden in Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="8c5d9-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8c5d9-241">Terwijl de SDK-tabelopslag biedt momenteel geen ondersteuning voor doorvoer wijzigen, kunt u de doorvoer onmiddellijk op elk gewenst moment met de Azure-portal of Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="8c5d9-242">Vervolgens we doorlopen van het eenvoudige lezen en schrijven (CRUD)-bewerkingen met de SDK van Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="8c5d9-243">Deze zelfstudie wordt gedemonstreerd voorspelbare lage één cijfer milliseconde latenties en snelle query's die worden geleverd door Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="8c5d9-244">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="8c5d9-244">Add an entity to a table</span></span>
<span data-ttu-id="8c5d9-245">Entiteiten in Azure Table storage uitbreiden van de `TableEntity` klasse en moet `PartitionKey` en `RowKey` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="8c5d9-246">Hier volgt een voorbeeld-definitie voor een klantentiteit.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="8c5d9-247">Het volgende fragment toont het invoegen van een entiteit met de Azure SDK-opslag.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="8c5d9-248">Azure Cosmos DB is ontworpen voor lage latentie op elke schaal gegarandeerd over de hele wereld.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="8c5d9-249">Schrijfbewerkingen voltooien < 15 ms op p99 en ~ 6 ms op p50 voor toepassingen die worden uitgevoerd in dezelfde regio bevinden als de Azure DB die Cosmos-account.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="8c5d9-250">En deze duur is verantwoordelijk voor het feit dat schrijfbewerkingen terug naar de client zijn bevestigd nadat ze zijn synchroon gerepliceerd, blijvend doorgevoerd, en alle inhoud wordt geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="8c5d9-251">De tabel-API voor Azure DB die Cosmos is een Preview-versie.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="8c5d9-252">Algemene beschikbaarheid worden de latentie p99 garanties ondersteund door serviceovereenkomsten net als andere Azure Cosmos DB-API's.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8c5d9-253">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-253">Insert a batch of entities</span></span>
<span data-ttu-id="8c5d9-254">Azure Table storage ondersteunt een batchbewerking API, waarmee u het combineren van updates, verwijderingen en invoegingen in dezelfde batchbewerking.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="8c5d9-255">Azure Cosmos DB heeft geen enkele beperkingen voor de batch-API als Azure Table storage.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="8c5d9-256">Bijvoorbeeld, kunt u meerdere leesbewerkingen binnen een batch uitvoeren, kunt u meerdere schrijfbewerkingen naar dezelfde entiteit binnen een batch uitvoeren en er is geen limiet van 100 bewerkingen per batch.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="8c5d9-257">Eén entiteit ophalen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-257">Retrieve a single entity</span></span>
<span data-ttu-id="8c5d9-258">(Opgehaald) opgehaald in Azure Cosmos DB voltooid < 10 ms op p99 en ~ 1 ms op p50 in dezelfde Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="8c5d9-259">U kunt zoveel regio's toevoegen aan uw account voor leesbewerkingen lage latentie en implementeren van toepassingen voor het lezen van de lokale regio ('multihomed') door in te stellen `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="8c5d9-260">U kunt met behulp van het volgende fragment één entiteit ophalen:</span><span class="sxs-lookup"><span data-stu-id="8c5d9-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="8c5d9-261">Meer informatie over multihoming API's op [ontwikkelen met meerdere regio's](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="8c5d9-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="8c5d9-262">Query-entiteiten met behulp van automatische secundaire indexen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="8c5d9-263">Tabellen kunnen worden opgevraagd met de `TableQuery` klasse.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="8c5d9-264">Azure Cosmos-database heeft een schrijven geoptimaliseerd database-engine die automatisch alle kolommen in de tabel indexeert.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="8c5d9-265">Indexeren in Azure DB die Cosmos is agnostisch ten opzichte van schema.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="8c5d9-266">Dus wordt zelfs als uw schema afwijkt van rijen, of als het schema gedurende een bepaalde periode zich verder ontwikkelen, deze automatisch geïndexeerd.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="8c5d9-267">Omdat Azure Cosmos DB automatische secundaire indexen ondersteunt, wordt een query uitgevoerd naar een eigenschap de index kunnen gebruiken en efficiënt worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

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

<span data-ttu-id="8c5d9-268">In preview ondersteunt Azure Cosmos DB dezelfde queryfunctionaliteit als Azure Table storage voor de tabel-API.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="8c5d9-269">Azure Cosmos DB biedt ook ondersteuning voor sorteren, statistische functies, georuimtelijke query hiërarchie en een groot aantal ingebouwde functies.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="8c5d9-270">De aanvullende functionaliteit worden vermeld in de tabel-API in een toekomstige service-update.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="8c5d9-271">Zie [Azure Cosmos DB-query](documentdb-sql-query.md) voor een overzicht van deze mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="8c5d9-272">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-272">Replace an entity</span></span>
<span data-ttu-id="8c5d9-273">Als u een entiteit wilt bijwerken, haalt u deze op uit de Tabelservice, wijzigt u het entiteitsobject en slaat u de wijzigingen weer op in de Tabelservice.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="8c5d9-274">De volgende code wijzigt het telefoonnummer van een bestaande klant.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="8c5d9-275">Op deze manier kunt u uitvoeren `InsertOrMerge` of `Merge` bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="8c5d9-276">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-276">Delete an entity</span></span>
<span data-ttu-id="8c5d9-277">U kunt een entiteit gemakkelijk verwijderen nadat u deze hebt opgehaald. Hiervoor gebruikt u hetzelfde patroon dat is getoond voor het bijwerken van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="8c5d9-278">Met de volgende code wordt een klantentiteit opgehaald en verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="8c5d9-279">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-279">Delete a table</span></span>
<span data-ttu-id="8c5d9-280">Ten slotte wordt met het volgende codevoorbeeld een tabel uit een opslagaccount verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="8c5d9-281">U kunt verwijderen en opnieuw maken van een tabel met Azure Cosmos DB onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="8c5d9-282">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-282">Clean up resources</span></span> 

<span data-ttu-id="8c5d9-283">Als u deze app verder niet gaat gebruiken, kunt u met de volgende stappen alle resources verwijderen die met deze zelfstudies in Azure Portal zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="8c5d9-284">Klik in het menu aan de linkerkant in Azure Portal op **Resourcegroepen** en klik vervolgens op de resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="8c5d9-285">Klik op de pagina van uw resourcegroep op **Verwijderen**, typ de naam van de resource die u wilt verwijderen in het tekstvak en klik vervolgens op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8c5d9-286">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-286">Next steps</span></span>

<span data-ttu-id="8c5d9-287">We hoe u aan de slag met Azure Cosmos DB met de API tabel behandeld in deze zelfstudie maakt en u het volgende hebt gedaan:</span><span class="sxs-lookup"><span data-stu-id="8c5d9-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="8c5d9-288">Een Azure DB die Cosmos-account gemaakt</span><span class="sxs-lookup"><span data-stu-id="8c5d9-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="8c5d9-289">Ingeschakelde functionaliteit in het bestand app.config</span><span class="sxs-lookup"><span data-stu-id="8c5d9-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="8c5d9-290">Een tabel gemaakt</span><span class="sxs-lookup"><span data-stu-id="8c5d9-290">Created a table</span></span> 
> * <span data-ttu-id="8c5d9-291">Een entiteit toegevoegd aan een tabel</span><span class="sxs-lookup"><span data-stu-id="8c5d9-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="8c5d9-292">Een batch entiteiten invoegen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="8c5d9-293">Één entiteit opgehaald</span><span class="sxs-lookup"><span data-stu-id="8c5d9-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="8c5d9-294">De query entiteiten met behulp van automatische secundaire indexen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="8c5d9-295">Een entiteit vervangen</span><span class="sxs-lookup"><span data-stu-id="8c5d9-295">Replaced an entity</span></span> 
> * <span data-ttu-id="8c5d9-296">Een entiteit wordt verwijderd</span><span class="sxs-lookup"><span data-stu-id="8c5d9-296">Deleted an entity</span></span> 
> * <span data-ttu-id="8c5d9-297">Een tabel verwijderd</span><span class="sxs-lookup"><span data-stu-id="8c5d9-297">Deleted a table</span></span>  

<span data-ttu-id="8c5d9-298">U kunt nu doorgaan met de volgende zelfstudie en meer informatie over het opvragen van tabelgegevens.</span><span class="sxs-lookup"><span data-stu-id="8c5d9-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8c5d9-299">Query met de tabel-API</span><span class="sxs-lookup"><span data-stu-id="8c5d9-299">Query with the Table API</span></span>](tutorial-query-table.md)
