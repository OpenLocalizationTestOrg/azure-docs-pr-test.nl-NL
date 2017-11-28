---
title: een database van de grafiek Azure Cosmos DB met Java aaaCreate | Microsoft Docs
description: Geeft een Java-code voorbeeld kunt u tooconnect tooand query grafiekgegevens in Azure Cosmos DB met Gremlin.
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="3c539-103">Azure Cosmos DB: Maak een graph-database met behulp van Java en hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3c539-103">Azure Cosmos DB: Create a graph database using Java and hello Azure portal</span></span>

<span data-ttu-id="3c539-104">Azure Cosmos DB is de wereldwijd gedistribueerde multimodel-databaseservice van Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3c539-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="3c539-105">U kunt snel maken en query document, de sleutel/waarde en de grafiek databases, die allemaal van Hallo wereldwijde distributie en mogelijkheden van de horizontale schaal Hallo kern van Azure Cosmos DB profiteren.</span><span class="sxs-lookup"><span data-stu-id="3c539-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="3c539-106">Deze snelstartgids maakt een grafiek database met Azure portal-hulpprogramma's Hallo voor Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="3c539-106">This quickstart creates a graph database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="3c539-107">Deze snelstartgids ook ziet u hoe tooquickly maken voor een Java-consoletoepassing met behulp van een graph-database met behulp van Hallo OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="3c539-107">This quickstart also shows you how tooquickly create a Java console app using a graph database using hello OSS [Gremlin Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) driver.</span></span> <span data-ttu-id="3c539-108">Hallo-instructies in deze snelstartgids kunnen worden uitgevoerd op elk besturingssysteem waarmee Java uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c539-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="3c539-109">Deze snelstartgids familiarizes u met het maken en wijzigen van de grafiek bronnen in de Hallo gebruikersinterface of via een programma, afhankelijk van wat uw voorkeur is.</span><span class="sxs-lookup"><span data-stu-id="3c539-109">This quickstart familiarizes you with creating and modifying graph resources in either hello UI or programmatically, whichever is your preference.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3c539-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c539-110">Prerequisites</span></span>

* [<span data-ttu-id="3c539-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="3c539-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="3c539-112">Voer op Ubuntu, `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="3c539-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="3c539-113">Worden ervoor tooset hello JAVA_HOME omgeving variabele toopoint toohello map is waarin Hallo JDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3c539-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="3c539-114">[Download](http://maven.apache.org/download.cgi) en [installeer](http://maven.apache.org/install.html) een binair [Maven](http://maven.apache.org/)-archief</span><span class="sxs-lookup"><span data-stu-id="3c539-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="3c539-115">Ubuntu, u kunt uitvoeren `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="3c539-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="3c539-116">Git</span><span class="sxs-lookup"><span data-stu-id="3c539-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="3c539-117">Ubuntu, u kunt uitvoeren `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="3c539-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="3c539-118">Een databaseaccount maken</span><span class="sxs-lookup"><span data-stu-id="3c539-118">Create a database account</span></span>

<span data-ttu-id="3c539-119">Voordat u een database van de grafiek maken kunt, moet u een databaseaccount Gremlin (grafiek) met Azure Cosmos DB toocreate.</span><span class="sxs-lookup"><span data-stu-id="3c539-119">Before you can create a graph database, you need toocreate a Gremlin (Graph) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="3c539-120">Een graaf toevoegen</span><span class="sxs-lookup"><span data-stu-id="3c539-120">Add a graph</span></span>

<span data-ttu-id="3c539-121">U kunt nu Hallo Data Explorer hulpprogramma gebruiken in hello Azure portal toocreate een graph-database.</span><span class="sxs-lookup"><span data-stu-id="3c539-121">You can now use hello Data Explorer tool in hello Azure portal toocreate a graph database.</span></span> 

1. <span data-ttu-id="3c539-122">Klik in de Azure-portal in links navigatiemenu Hallo Hallo op **Data Explorer (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="3c539-122">In hello Azure portal, in hello left navigation menu, click **Data Explorer (Preview)**.</span></span> 
2. <span data-ttu-id="3c539-123">In Hallo **Data Explorer (Preview)** blade, klikt u op **nieuwe grafiek**, vul vervolgens met behulp van de volgende informatie Hallo Hallo-pagina:</span><span class="sxs-lookup"><span data-stu-id="3c539-123">In hello **Data Explorer (Preview)** blade, click **New Graph**, then fill in hello page using hello following information:</span></span>

    ![Data Explorer in hello Azure-portal](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    <span data-ttu-id="3c539-125">Instelling</span><span class="sxs-lookup"><span data-stu-id="3c539-125">Setting</span></span>|<span data-ttu-id="3c539-126">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="3c539-126">Suggested value</span></span>|<span data-ttu-id="3c539-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3c539-127">Description</span></span>
    ---|---|---
    <span data-ttu-id="3c539-128">Database-id</span><span class="sxs-lookup"><span data-stu-id="3c539-128">Database ID</span></span>|<span data-ttu-id="3c539-129">voorbeelddatabase</span><span class="sxs-lookup"><span data-stu-id="3c539-129">sample-database</span></span>|<span data-ttu-id="3c539-130">Hallo-ID voor de nieuwe database.</span><span class="sxs-lookup"><span data-stu-id="3c539-130">hello ID for your new database.</span></span> <span data-ttu-id="3c539-131">Databasenamen moeten tussen de 1 en 255 tekens zijn en mogen geen `/ \ # ?` bevatten of eindigen op een spatie.</span><span class="sxs-lookup"><span data-stu-id="3c539-131">Database names must be between 1 and 255 characters, and cannot contain `/ \ # ?` or a trailing space.</span></span>
    <span data-ttu-id="3c539-132">Grafiek-id</span><span class="sxs-lookup"><span data-stu-id="3c539-132">Graph ID</span></span>|<span data-ttu-id="3c539-133">voorbeeldgrafiek</span><span class="sxs-lookup"><span data-stu-id="3c539-133">sample-graph</span></span>|<span data-ttu-id="3c539-134">Hallo-ID voor de nieuwe grafiek.</span><span class="sxs-lookup"><span data-stu-id="3c539-134">hello ID for your new graph.</span></span> <span data-ttu-id="3c539-135">Namen van de grafiek Hallo hebben dezelfde vereisten als de database-id's teken.</span><span class="sxs-lookup"><span data-stu-id="3c539-135">Graph names have hello same character requirements as database ids.</span></span>
    <span data-ttu-id="3c539-136">Opslagcapaciteit</span><span class="sxs-lookup"><span data-stu-id="3c539-136">Storage Capacity</span></span>| <span data-ttu-id="3c539-137">10 GB</span><span class="sxs-lookup"><span data-stu-id="3c539-137">10 GB</span></span>|<span data-ttu-id="3c539-138">Laat de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c539-138">Leave hello default value.</span></span> <span data-ttu-id="3c539-139">Dit is de opslagcapaciteit Hallo van Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="3c539-139">This is hello storage capacity of hello database.</span></span>
    <span data-ttu-id="3c539-140">Doorvoer</span><span class="sxs-lookup"><span data-stu-id="3c539-140">Throughput</span></span>|<span data-ttu-id="3c539-141">400 RU‘s</span><span class="sxs-lookup"><span data-stu-id="3c539-141">400 RUs</span></span>|<span data-ttu-id="3c539-142">Laat de standaardwaarde Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c539-142">Leave hello default value.</span></span> <span data-ttu-id="3c539-143">U kunt opschalen doorvoer hello later als u wilt dat tooreduce latentie.</span><span class="sxs-lookup"><span data-stu-id="3c539-143">You can scale up hello throughput later if you want tooreduce latency.</span></span>
    <span data-ttu-id="3c539-144">Partitiesleutel</span><span class="sxs-lookup"><span data-stu-id="3c539-144">Partition key</span></span>|<span data-ttu-id="3c539-145">Leeg laten</span><span class="sxs-lookup"><span data-stu-id="3c539-145">Leave blank</span></span>|<span data-ttu-id="3c539-146">Hallo-doel van deze snelstartgids, Hallo partitiesleutel leeg laten.</span><span class="sxs-lookup"><span data-stu-id="3c539-146">For hello purpose of this quickstart, leave hello partition key blank.</span></span>

3. <span data-ttu-id="3c539-147">Zodra het Hallo-formulier wordt ingevuld, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c539-147">Once hello form is filled out, click **OK**.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="3c539-148">Hallo-voorbeeldtoepassing klonen</span><span class="sxs-lookup"><span data-stu-id="3c539-148">Clone hello sample application</span></span>

<span data-ttu-id="3c539-149">Nu gaan we een graph-app vanuit github Hallo verbindingsreeks instellen en voer dit klonen.</span><span class="sxs-lookup"><span data-stu-id="3c539-149">Now let's clone a graph app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="3c539-150">U ziet hoe eenvoudig het is toowork met gegevens via een programma.</span><span class="sxs-lookup"><span data-stu-id="3c539-150">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="3c539-151">Open een git-terminalvenster zoals git bash en en `cd` tooa werkmap.</span><span class="sxs-lookup"><span data-stu-id="3c539-151">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="3c539-152">Hallo na de opdracht tooclone Hallo voorbeeld opslagplaats worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c539-152">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="3c539-153">Hallo code bekijken</span><span class="sxs-lookup"><span data-stu-id="3c539-153">Review hello code</span></span>

<span data-ttu-id="3c539-154">We maken een kort overzicht van wat in Hallo-app gebeurt er.</span><span class="sxs-lookup"><span data-stu-id="3c539-154">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="3c539-155">Open Hallo `Program.java` bestand van Hallo \src\GetStarted map en deze regels code vinden.</span><span class="sxs-lookup"><span data-stu-id="3c539-155">Open hello `Program.java` file from hello \src\GetStarted folder and find these lines of code.</span></span> 

* <span data-ttu-id="3c539-156">Hallo Gremlin `Client` wordt geïnitialiseerd vanuit Hallo-configuratie in `src/remote.yaml`.</span><span class="sxs-lookup"><span data-stu-id="3c539-156">hello Gremlin `Client` is initialized from hello configuration in `src/remote.yaml`.</span></span>

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* <span data-ttu-id="3c539-157">Een reeks Gremlin stappen worden uitgevoerd met Hallo `client.submit` methode.</span><span class="sxs-lookup"><span data-stu-id="3c539-157">A series of Gremlin steps are executed using hello `client.submit` method.</span></span>

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="3c539-158">Uw verbindingsreeks bijwerken</span><span class="sxs-lookup"><span data-stu-id="3c539-158">Update your connection string</span></span>

1. <span data-ttu-id="3c539-159">Open Hallo src/remote.yaml-bestand.</span><span class="sxs-lookup"><span data-stu-id="3c539-159">Open hello src/remote.yaml file.</span></span> 

3. <span data-ttu-id="3c539-160">Vul uw *hosts*, *gebruikersnaam*, en *wachtwoord* waarden in Hallo src/remote.yaml bestand.</span><span class="sxs-lookup"><span data-stu-id="3c539-160">Fill in your *hosts*, *username*, and *password* values in hello src/remote.yaml file.</span></span> <span data-ttu-id="3c539-161">Hallo rest Hallo instellingen hoeven niet toobe gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="3c539-161">hello rest of hello settings do not need toobe changed.</span></span>

    <span data-ttu-id="3c539-162">Instelling</span><span class="sxs-lookup"><span data-stu-id="3c539-162">Setting</span></span>|<span data-ttu-id="3c539-163">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="3c539-163">Suggested value</span></span>|<span data-ttu-id="3c539-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3c539-164">Description</span></span>
    ---|---|---
    <span data-ttu-id="3c539-165">Hosts</span><span class="sxs-lookup"><span data-stu-id="3c539-165">Hosts</span></span>|<span data-ttu-id="3c539-166">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="3c539-166">[***.graphs.azure.com]</span></span>|<span data-ttu-id="3c539-167">Zie Hallo schermafbeelding onder deze tabel.</span><span class="sxs-lookup"><span data-stu-id="3c539-167">See hello screenshot following this table.</span></span> <span data-ttu-id="3c539-168">Deze waarde is Hallo Gremlin URI-waarde op de overzichtspagina Hallo Hallo Azure-portal tussen vierkante haken met hallo afsluitende: 443 / verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3c539-168">This value is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="3c539-169">Deze waarde kan ook worden opgehaald uit Hallo sleutels tabblad Hallo URI-waarde met https:// te verwijderen, documenten toographs wijzigen en verwijderen van Hallo afsluitende: 443 /.</span><span class="sxs-lookup"><span data-stu-id="3c539-169">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="3c539-170">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="3c539-170">Username</span></span>|<span data-ttu-id="3c539-171">/dbs/sample-database/colls/sample-graph</span><span class="sxs-lookup"><span data-stu-id="3c539-171">/dbs/sample-database/colls/sample-graph</span></span>|<span data-ttu-id="3c539-172">bron van het formulier Hallo Hallo `/dbs/<db>/colls/<coll>` waar `<db>` is de databasenaam van uw bestaande en `<coll>` is de Collectienaam van uw bestaande.</span><span class="sxs-lookup"><span data-stu-id="3c539-172">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your existing database name and `<coll>` is your existing collection name.</span></span>
    <span data-ttu-id="3c539-173">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="3c539-173">Password</span></span>|<span data-ttu-id="3c539-174">*Uw primaire hoofdsleutel*</span><span class="sxs-lookup"><span data-stu-id="3c539-174">*Your primary master key*</span></span>|<span data-ttu-id="3c539-175">Zie de tweede schermafbeelding Hallo onder deze tabel.</span><span class="sxs-lookup"><span data-stu-id="3c539-175">See hello second screenshot following this table.</span></span> <span data-ttu-id="3c539-176">Deze waarde is de primaire sleutel, die u uit Hallo sleutels pagina Hallo in Hallo primaire sleutel in Azure portal ophalen kunt.</span><span class="sxs-lookup"><span data-stu-id="3c539-176">This value is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="3c539-177">Hallo-waarde met behulp van de knop kopiëren Hallo aan de rechterkant Hallo van Hallo vak kopiëren.</span><span class="sxs-lookup"><span data-stu-id="3c539-177">Copy hello value using hello copy button on hello right side of hello box.</span></span>

    <span data-ttu-id="3c539-178">Voor Hallo Hosts waarde, kopieert u Hallo **Gremlin URI** waarde van Hallo **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="3c539-178">For hello Hosts value, copy hello **Gremlin URI** value from hello **Overview** page.</span></span> <span data-ttu-id="3c539-179">Zie Hallo-instructies in Hallo Hosts rij in de voorgaande tabel over het maken van Hallo Gremlin URI van de blade sleutels Hallo Hallo als deze leeg is.</span><span class="sxs-lookup"><span data-stu-id="3c539-179">If it's empty, see hello instructions in hello Hosts row in hello preceding table about creating hello Gremlin URI from hello Keys blade.</span></span>
<span data-ttu-id="3c539-180">![Weergeven en kopiëren Hallo Gremlin URI-waarde op de overzichtspagina Hallo in hello Azure-portal](./media/create-graph-java/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="3c539-180">![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-java/gremlin-uri.png)</span></span>

    <span data-ttu-id="3c539-181">Voor Hallo waarde wachtwoord, kopieert u Hallo **primaire sleutel** van Hallo **sleutels** blade: ![weergeven en kopieer de primaire sleutel in hello Azure-portal, sleutels pagina](./media/create-graph-java/keys.png)</span><span class="sxs-lookup"><span data-stu-id="3c539-181">For hello Password value, copy hello **Primary key** from hello **Keys** blade: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-java/keys.png)</span></span>

## <a name="run-hello-console-app"></a><span data-ttu-id="3c539-182">Hallo-console-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3c539-182">Run hello console app</span></span>

1. <span data-ttu-id="3c539-183">In Hallo git terminalvenster, `cd` toohello azure-cosmos-db-graph-java-getting-started map.</span><span class="sxs-lookup"><span data-stu-id="3c539-183">In hello git terminal window, `cd` toohello azure-cosmos-db-graph-java-getting-started folder.</span></span>

2. <span data-ttu-id="3c539-184">Typ in het Hallo git terminalvenster, `mvn package` tooinstall Hallo vereist Java-pakketten.</span><span class="sxs-lookup"><span data-stu-id="3c539-184">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="3c539-185">Voer in Hallo git terminalvenster, `mvn exec:java -D exec.mainClass=GetStarted.Program` in Hallo terminalvenster toostart uw Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c539-185">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

<span data-ttu-id="3c539-186">Hallo terminalvenster geeft Hallo hoekpunten toohello grafiek worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3c539-186">hello terminal window displays hello vertices being added toohello graph.</span></span> <span data-ttu-id="3c539-187">Eenmaal Hallo programma is voltooid, schakelt u back-toohello Azure-portal in uw internetbrowser.</span><span class="sxs-lookup"><span data-stu-id="3c539-187">Once hello program completes, switch back toohello Azure portal in your internet browser.</span></span> 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a><span data-ttu-id="3c539-188">Voorbeeldgegevens bekijken en toevoegen</span><span class="sxs-lookup"><span data-stu-id="3c539-188">Review and add sample data</span></span>

<span data-ttu-id="3c539-189">U kunt nu gaat u terug tooData Explorer en Zie Hallo hoekpunten toohello grafiek toegevoegd en voeg extra gegevenspunten.</span><span class="sxs-lookup"><span data-stu-id="3c539-189">You can now go back tooData Explorer and see hello vertices added toohello graph, and add additional data points.</span></span>

1. <span data-ttu-id="3c539-190">Vouw in de Data Explorer Hallo **-voorbeelddatabase**/**voorbeeld grafiek**, klikt u op **grafiek**, en klik vervolgens op **Filter toepassen**.</span><span class="sxs-lookup"><span data-stu-id="3c539-190">In Data Explorer, expand hello **sample-database**/**sample-graph**, click **Graph**, and then click **Apply Filter**.</span></span> 

   ![Maken van nieuwe documenten in de Data Explorer in hello Azure-portal](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. <span data-ttu-id="3c539-192">In Hallo **resultaten** lijst, Hallo nieuwe gebruikers toegevoegd toohello grafiek.</span><span class="sxs-lookup"><span data-stu-id="3c539-192">In hello **Results** list, notice hello new users added toohello graph.</span></span> <span data-ttu-id="3c539-193">Selecteer **ben** ziet u dat hij toorobin is verbonden.</span><span class="sxs-lookup"><span data-stu-id="3c539-193">Select **ben** and notice that he's connected toorobin.</span></span> <span data-ttu-id="3c539-194">U kunt Hallo hoekpunten verplaatsen op Hallo grafiek explorer, in-en uitzoomen, uitvouwen en grootte van Hallo grafiek explorer oppervlak Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c539-194">You can move hello vertices around on hello graph explorer, zoom in and out, and expand hello size of hello graph explorer surface.</span></span> 

   ![Nieuwe hoekpunten in de grafiek Hallo in Data Explorer in hello Azure-portal](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. <span data-ttu-id="3c539-196">Laten we enkele nieuwe gebruikers toohello grafiek met Hallo Data Explorer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3c539-196">Let's add a few new users toohello graph using hello Data Explorer.</span></span> <span data-ttu-id="3c539-197">Klik op Hallo **nieuw hoekpunt** knop tooadd gegevens tooyour grafiek.</span><span class="sxs-lookup"><span data-stu-id="3c539-197">Click hello **New Vertex** button tooadd data tooyour graph.</span></span>

   ![Maken van nieuwe documenten in de Data Explorer in hello Azure-portal](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. <span data-ttu-id="3c539-199">Voer een label van *persoon* Voer Hallo volgende sleutels en waarden toocreate Hallo eerste hoekpunt in Hallo-grafiek.</span><span class="sxs-lookup"><span data-stu-id="3c539-199">Enter a label of *person* then enter hello following keys and values toocreate hello first vertex in hello graph.</span></span> <span data-ttu-id="3c539-200">U kunt unieke eigenschappen maken voor elke persoon in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="3c539-200">Notice that you can create unique properties for each person in your graph.</span></span> <span data-ttu-id="3c539-201">Alleen Hallo-id sleutel is vereist.</span><span class="sxs-lookup"><span data-stu-id="3c539-201">Only hello id key is required.</span></span>

    <span data-ttu-id="3c539-202">sleutel</span><span class="sxs-lookup"><span data-stu-id="3c539-202">key</span></span>|<span data-ttu-id="3c539-203">waarde</span><span class="sxs-lookup"><span data-stu-id="3c539-203">value</span></span>|<span data-ttu-id="3c539-204">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3c539-204">Notes</span></span>
    ----|----|----
    <span data-ttu-id="3c539-205">id</span><span class="sxs-lookup"><span data-stu-id="3c539-205">id</span></span>|<span data-ttu-id="3c539-206">ashley</span><span class="sxs-lookup"><span data-stu-id="3c539-206">ashley</span></span>|<span data-ttu-id="3c539-207">Hallo unieke id voor Hallo hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="3c539-207">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="3c539-208">Als u geen id opgeeft, wordt er een id voor u gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3c539-208">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="3c539-209">geslacht</span><span class="sxs-lookup"><span data-stu-id="3c539-209">gender</span></span>|<span data-ttu-id="3c539-210">vrouwelijk</span><span class="sxs-lookup"><span data-stu-id="3c539-210">female</span></span>| 
    <span data-ttu-id="3c539-211">technisch</span><span class="sxs-lookup"><span data-stu-id="3c539-211">tech</span></span> | <span data-ttu-id="3c539-212">java</span><span class="sxs-lookup"><span data-stu-id="3c539-212">java</span></span> | 

    > [!NOTE]
    > <span data-ttu-id="3c539-213">In deze snelstartgids maken we een niet-gepartitioneerde verzameling.</span><span class="sxs-lookup"><span data-stu-id="3c539-213">In this quickstart we create a non-partitioned collection.</span></span> <span data-ttu-id="3c539-214">Echter, als u een gepartitioneerde verzameling maken door op te geven van een partitiesleutel tijdens het maken van de verzameling hello, moet u tooinclude Hallo partitiesleutel als de sleutel in elk nieuw hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="3c539-214">However, if you create a partitioned collection by specifying a partition key during hello collection creation, then you need tooinclude hello partition key as a key in each new vertex.</span></span> 

5. <span data-ttu-id="3c539-215">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c539-215">Click **OK**.</span></span> <span data-ttu-id="3c539-216">Mogelijk moet u tooexpand uw scherm toosee **OK** op Hallo onderaan welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="3c539-216">You may need tooexpand your screen toosee **OK** on hello bottom of hello screen.</span></span>

6. <span data-ttu-id="3c539-217">Klik op **Nieuw hoekpunt** en voeg nog een nieuwe gebruiker toe.</span><span class="sxs-lookup"><span data-stu-id="3c539-217">Click **New Vertex** again and add an additional new user.</span></span> <span data-ttu-id="3c539-218">Voer een label van *persoon* voert u de volgende Hallo sleutels en waarden:</span><span class="sxs-lookup"><span data-stu-id="3c539-218">Enter a label of *person* then enter hello following keys and values:</span></span>

    <span data-ttu-id="3c539-219">sleutel</span><span class="sxs-lookup"><span data-stu-id="3c539-219">key</span></span>|<span data-ttu-id="3c539-220">waarde</span><span class="sxs-lookup"><span data-stu-id="3c539-220">value</span></span>|<span data-ttu-id="3c539-221">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="3c539-221">Notes</span></span>
    ----|----|----
    <span data-ttu-id="3c539-222">id</span><span class="sxs-lookup"><span data-stu-id="3c539-222">id</span></span>|<span data-ttu-id="3c539-223">rakesh</span><span class="sxs-lookup"><span data-stu-id="3c539-223">rakesh</span></span>|<span data-ttu-id="3c539-224">Hallo unieke id voor Hallo hoekpunt.</span><span class="sxs-lookup"><span data-stu-id="3c539-224">hello unique identifier for hello vertex.</span></span> <span data-ttu-id="3c539-225">Als u geen id opgeeft, wordt er een id voor u gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="3c539-225">If you don't specify an id, one is generated for you.</span></span>
    <span data-ttu-id="3c539-226">geslacht</span><span class="sxs-lookup"><span data-stu-id="3c539-226">gender</span></span>|<span data-ttu-id="3c539-227">man</span><span class="sxs-lookup"><span data-stu-id="3c539-227">male</span></span>| 
    <span data-ttu-id="3c539-228">school</span><span class="sxs-lookup"><span data-stu-id="3c539-228">school</span></span>|<span data-ttu-id="3c539-229">MIT</span><span class="sxs-lookup"><span data-stu-id="3c539-229">MIT</span></span>| 

7. <span data-ttu-id="3c539-230">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c539-230">Click **OK**.</span></span> 

8. <span data-ttu-id="3c539-231">Klik op **Filter toepassen** met Hallo standaard `g.V()` filter.</span><span class="sxs-lookup"><span data-stu-id="3c539-231">Click **Apply Filter** with hello default `g.V()` filter.</span></span> <span data-ttu-id="3c539-232">Alle Hallo gebruikers nu worden weergegeven in Hallo **resultaten** lijst.</span><span class="sxs-lookup"><span data-stu-id="3c539-232">All of hello users now show in hello **Results** list.</span></span> <span data-ttu-id="3c539-233">Als u meer gegevens toevoegt, kunt u filters toolimit uw resultaten.</span><span class="sxs-lookup"><span data-stu-id="3c539-233">As you add more data, you can use filters toolimit your results.</span></span> <span data-ttu-id="3c539-234">Data Explorer gebruikt standaard `g.V()` tooretrieve alle hoekpunten van een grafiek, maar u kunnen wijzigen die andere tooa [grafiek query](tutorial-query-graph.md), zoals `g.V().count()`, tooreturn een telling van alle Hallo hoekpunten van de grafiek Hallo in JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="3c539-234">By default, Data Explorer uses `g.V()` tooretrieve all vertices in a graph, but you can change that tooa different [graph query](tutorial-query-graph.md), such as `g.V().count()`, tooreturn a count of all hello vertices in hello graph in JSON format.</span></span>

9. <span data-ttu-id="3c539-235">Nu kunnen we rakesh en ashley met elkaar verbinden.</span><span class="sxs-lookup"><span data-stu-id="3c539-235">Now we can connect rakesh and ashley.</span></span> <span data-ttu-id="3c539-236">Zorg ervoor dat **Pascaline** in geselecteerd in Hallo **resultaten** lijst en klik op de knop bewerken Hallo volgende te**doelen** lagere rechts op.</span><span class="sxs-lookup"><span data-stu-id="3c539-236">Ensure **ashley** in selected in hello **Results** list, then click hello edit button next too**Targets** on lower right side.</span></span> <span data-ttu-id="3c539-237">Mogelijk moet u toowiden uw venster toosee hello **eigenschappen** gebied.</span><span class="sxs-lookup"><span data-stu-id="3c539-237">You may need toowiden your window toosee hello **Properties** area.</span></span>

   ![Hallo-doel van een hoekpunt in een grafiek wijzigen](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. <span data-ttu-id="3c539-239">In Hallo **doel** vak type *rakesh*, en in Hallo **rand label** vak type *kent*, en klik vervolgens op het selectievakje Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c539-239">In hello **Target** box type *rakesh*, and in hello **Edge label** box type *knows*, and then click hello check box.</span></span>

   ![Een verbinding tussen ashley en rakesh toevoegen in Data Explorer](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. <span data-ttu-id="3c539-241">Nu selecteren **rakesh** uit de lijst met resultaten Hallo en om te zien of Pascaline en rakesh zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="3c539-241">Now select **rakesh** from hello results list and see that ashley and rakesh are connected.</span></span> 

   ![Twee hoekpunten die zijn verbonden in Data Explorer](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    <span data-ttu-id="3c539-243">U kunt ook Data Explorer toocreate opgeslagen procedures, UDF's en triggers tooperform-bedrijfslogica server ook gebruiken als de doorvoer van de schaal.</span><span class="sxs-lookup"><span data-stu-id="3c539-243">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="3c539-244">Data Explorer toont alle Hallo ingebouwde programmatische toegang tot gegevens beschikbaar zijn in Hallo API's, maar biedt eenvoudige toegang tooyour gegevens in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3c539-244">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>



## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="3c539-245">Sla's bekijken in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="3c539-245">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="3c539-246">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="3c539-246">Clean up resources</span></span>

<span data-ttu-id="3c539-247">Als u deze app niet toocontinue toouse gaat, verwijdert u alle resources die zijn gemaakt door deze snelstartgids in hello Azure-portal met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c539-247">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span> 

1. <span data-ttu-id="3c539-248">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op Hallo-naam van het Hallo-resource die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c539-248">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="3c539-249">Klik op de pagina van de groep resource **verwijderen**, typ de naam Hallo van Hallo resource toodelete in Hallo tekstvak en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="3c539-249">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c539-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c539-250">Next steps</span></span>

<span data-ttu-id="3c539-251">In deze snelstartgids hebt u geleerd hoe toocreate een Cosmos-DB Azure-account maken van een grafiek met Hallo Data Explorer en een app uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3c539-251">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="3c539-252">U kunt nu complexere query's maken en met Gremlin krachtige logica implementeren om door een graaf te gaan.</span><span class="sxs-lookup"><span data-stu-id="3c539-252">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c539-253">Query’s uitvoeren met Gremlin</span><span class="sxs-lookup"><span data-stu-id="3c539-253">Query using Gremlin</span></span>](tutorial-query-graph.md)

