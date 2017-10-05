---
title: Zelfstudie over het ontwikkelen van Java-toepassingen met Azure Cosmos DB | Microsoft Docs
description: Deze zelfstudie over Java-webtoepassingen ziet u het gebruik van de Cosmos Azure DB en de DocumentDB-API voor het opslaan van en toegang tot gegevens uit een Java-toepassing gehost op Azure Websites.
keywords: Toepassingsontwikkeling, databasezelfstudie, java-toepassing, java-webtoepassing zelfstudie, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: 292115b5603c6f05a5eab3492d4b3e2096b58ed2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-the-documentdb-api"></a><span data-ttu-id="eddef-104">Een Java-webtoepassing met behulp van Azure DB die Cosmos en de API DocumentDB bouwen</span><span class="sxs-lookup"><span data-stu-id="eddef-104">Build a Java web application using Azure Cosmos DB and the DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eddef-105">.NET</span><span class="sxs-lookup"><span data-stu-id="eddef-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="eddef-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="eddef-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="eddef-107">Java</span><span class="sxs-lookup"><span data-stu-id="eddef-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="eddef-108">Python</span><span class="sxs-lookup"><span data-stu-id="eddef-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="eddef-109">Deze zelfstudie over Java-webtoepassingen, leest u hoe u de [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service voor het opslaan en toegang tot gegevens van een Java-toepassing die worden gehost op Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="eddef-109">This Java web application tutorial shows you how to use the [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service to store and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="eddef-110">In dit onderwerp leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="eddef-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="eddef-111">Het bouwen van een eenvoudige toepassing Java Server Pages (JSP) in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="eddef-111">How to build a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="eddef-112">Werken met de Azure Cosmos DB-service met behulp van de [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="eddef-112">How to work with the Azure Cosmos DB service using the [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="eddef-113">In deze zelfstudie over het maken van een Java-toepassing wordt uitgelegd hoe u een webtoepassing voor taakbeheer maakt waarmee u taken kunt maken, ophalen en als voltooid kunt markeren, zoals in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="eddef-113">This Java application tutorial shows you how to create a web-based task-management application that enables you to create, retrieve, and mark tasks as complete, as shown in the following image.</span></span> <span data-ttu-id="eddef-114">Alle taken in de ToDo-lijst worden als JSON-documenten opgeslagen in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eddef-114">Each of the tasks in the ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![De Java-toepassing My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="eddef-116">In deze zelfstudie voor het ontwikkelen van toepassingen wordt ervan uitgegaan dat u ervaring met Java hebt.</span><span class="sxs-lookup"><span data-stu-id="eddef-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="eddef-117">Als u niet bekend bent met Java of de [vereiste hulpprogramma's](#Prerequisites), is het raadzaam het volledige [todo](https://github.com/Azure-Samples/documentdb-java-todo-app)-project via GitHub te downloaden. Vervolgens kunt u [de instructies aan het eind van dit artikel gebruiken](#GetProject) om het project op te bouwen.</span><span class="sxs-lookup"><span data-stu-id="eddef-117">If you are new to Java or the [prerequisite tools](#Prerequisites), we recommend downloading the complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [the instructions at the end of this article](#GetProject).</span></span> <span data-ttu-id="eddef-118">Zodra u klaar bent, kunt u het artikel lezen voor meer informatie over de code in de context van het project.</span><span class="sxs-lookup"><span data-stu-id="eddef-118">Once you have it built, you can review the article to gain insight on the code in the context of the project.</span></span>  
> 
> 

## <span data-ttu-id="eddef-119"><a id="Prerequisites"></a>Vereisten voor deze zelfstudie over Java-webtoepassingen</span><span class="sxs-lookup"><span data-stu-id="eddef-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="eddef-120">Voordat u met deze zelfstudie over het ontwikkelen van toepassingen aan de slag gaat, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="eddef-120">Before you begin this application development tutorial, you must have the following:</span></span>

* <span data-ttu-id="eddef-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="eddef-121">An active Azure account.</span></span> <span data-ttu-id="eddef-122">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="eddef-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="eddef-123">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="eddef-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="eddef-124">OF</span><span class="sxs-lookup"><span data-stu-id="eddef-124">OR</span></span>

    <span data-ttu-id="eddef-125">Een lokale installatie van de [Azure Cosmos DB-emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="eddef-125">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="eddef-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="eddef-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="eddef-127">Eclipse IDE voor Java EE-ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="eddef-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="eddef-128">Een Azure-website met een Java runtime environment (bijvoorbeeld Tomcat of Jetty) is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="eddef-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="eddef-129">Als u deze hulpprogramma's voor het eerst installeert, kunt u op coreservlets.com in de Quick Start-sectie van het artikel[Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) (Zelfstudie: TomCat7 installeren en gebruiken met Eclipse) een overzicht van het installatieproces vinden.</span><span class="sxs-lookup"><span data-stu-id="eddef-129">If you're installing these tools for the first time, coreservlets.com provides a walk-through of the installation process in the Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="eddef-130"><a id="CreateDB"></a>Stap 1: Een Azure DB die Cosmos-account maken</span><span class="sxs-lookup"><span data-stu-id="eddef-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="eddef-131">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="eddef-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="eddef-132">Als u al een account hebt of de Azure Cosmos DB-emulator gebruikt voor deze zelfstudie, kunt u direct doorgaan naar [Stap 2: de Java JSP-toepassing maken](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="eddef-132">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create the Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="eddef-133"><a id="CreateJSP"></a>Stap 2: De Java JSP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="eddef-133"><a id="CreateJSP"></a>Step 2: Create the Java JSP application</span></span>
<span data-ttu-id="eddef-134">De JSP-toepassing maken:</span><span class="sxs-lookup"><span data-stu-id="eddef-134">To create the JSP application:</span></span>

1. <span data-ttu-id="eddef-135">Als eerste moet u een Java-project maken.</span><span class="sxs-lookup"><span data-stu-id="eddef-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="eddef-136">Start Eclipse en klik achtereenvolgens op **File** (Bestand), **New** (Nieuw) en **Dynamic Web Project** (Dynamisch webproject).</span><span class="sxs-lookup"><span data-stu-id="eddef-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="eddef-137">Als er geen **dynamisch webproject** beschikbaar is, gaat u als volg te werk: klik achtereenvolgens op **File** (Bestand), **New** (Nieuw), **Project**, vouw **Web** uit en klik op **Dynamic Web Project** (Dynamische webproject) en **Next** (Volgende).</span><span class="sxs-lookup"><span data-stu-id="eddef-137">If you don’t see **Dynamic Web Project** listed as an available project, do the following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java-toepassing ontwikkelen](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="eddef-139">Voer in het vak **Project name** (Projectnaam) een projectnaam in en selecteer in de vervolgkeuzelijst **Target Runtime** (Doelruntime) eventueel een waarde (bijvoorbeeld Apache Tomcat v7.0) en klik vervolgens op **Finish** (Voltooien).</span><span class="sxs-lookup"><span data-stu-id="eddef-139">Enter a project name in the **Project name** box, and in the **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="eddef-140">Door een doelruntime te selecteren, kunt u het project lokaal via Eclipse uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="eddef-140">Selecting a target runtime enables you to run your project locally through Eclipse.</span></span>
3. <span data-ttu-id="eddef-141">Vouw in de weergave Project Explorer (Projectverkenner) van Eclipse uw project uit.</span><span class="sxs-lookup"><span data-stu-id="eddef-141">In Eclipse, in the Project Explorer view, expand your project.</span></span> <span data-ttu-id="eddef-142">Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).</span><span class="sxs-lookup"><span data-stu-id="eddef-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="eddef-143">Geef in het dialoogvenster **New JSP File** (Nieuw JSP-bestand) de naam **index.jsp** voor het bestand op.</span><span class="sxs-lookup"><span data-stu-id="eddef-143">In the **New JSP File** dialog box, name the file **index.jsp**.</span></span> <span data-ttu-id="eddef-144">Bewaar de bovenliggende map als **WebContent**, zoals weergegeven in de volgende afbeelding, en klik vervolgens op **Next** (Volgende).</span><span class="sxs-lookup"><span data-stu-id="eddef-144">Keep the parent folder as **WebContent**, as shown in the following illustration, and then click **Next**.</span></span>
   
    ![Een nieuw JSP-bestand maken - Zelfstudie Java-webtoepassing](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="eddef-146">Selecteer voor deze zelfstudie in het dialoogvenster **Select JSP Template** (JSP-sjabloon selecteren) de optie **New JSP File (html)** (Nieuw JSP-bestand (html)) en klik vervolgens op **Finish** (Voltooien).</span><span class="sxs-lookup"><span data-stu-id="eddef-146">In the **Select JSP Template** dialog box, for the purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="eddef-147">Wanneer het bestand index.jsp wordt geopend in Eclipse, voegt u tekst toe om **Hello World!** weer te geven</span><span class="sxs-lookup"><span data-stu-id="eddef-147">When the index.jsp file opens in Eclipse, add text to display **Hello World!**</span></span> <span data-ttu-id="eddef-148">in het bestaande <body>-element.</span><span class="sxs-lookup"><span data-stu-id="eddef-148">within the existing <body> element.</span></span> <span data-ttu-id="eddef-149">Uw bijgewerkte <body>-inhoud moet eruitzien als de volgende code:</span><span class="sxs-lookup"><span data-stu-id="eddef-149">Your updated <body> content should look like the following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="eddef-150">Sla het bestand index.jsp op.</span><span class="sxs-lookup"><span data-stu-id="eddef-150">Save the index.jsp file.</span></span>
8. <span data-ttu-id="eddef-151">Als u een doelruntime in stap 2 hebt ingesteld, kunt u achtereenvolgens op **Project** en **Run** klikken om uw JSP-toepassing lokaal uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eddef-151">If you set a target runtime in step 2, you can click **Project** and then **Run** to run your JSP application locally:</span></span>
   
    ![Hello World – Zelfstudie Java-toepassing](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="eddef-153"><a id="InstallSDK"></a>Stap 3: De DocumentDB Java SDK installeren</span><span class="sxs-lookup"><span data-stu-id="eddef-153"><a id="InstallSDK"></a>Step 3: Install the DocumentDB Java SDK</span></span>
<span data-ttu-id="eddef-154">De eenvoudigste manier om de Java DocumentDB SDK en de bijbehorende afhankelijkheden op te halen, is via [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="eddef-154">The easiest way to pull in the DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="eddef-155">Hiervoor moet u de volgende stappen uitvoeren om het project te converteren naar een Maven-project:</span><span class="sxs-lookup"><span data-stu-id="eddef-155">To do this, you will need to convert your project to a maven project by completing the following steps:</span></span>

1. <span data-ttu-id="eddef-156">Klik met de rechtermuisknop in de Projectverkenner, klik op **Configure** (Configureren) en klik vervolgens op **Convert to Maven Project** (Configureren naar een Maven-project).</span><span class="sxs-lookup"><span data-stu-id="eddef-156">Right-click your project in the Project Explorer, click **Configure**, click **Convert to Maven Project**.</span></span>
2. <span data-ttu-id="eddef-157">Accepteer in het venster **Create new POM** (Nieuwe POM maken) de standaardinstellingen en klik op **Finish** (Voltooien).</span><span class="sxs-lookup"><span data-stu-id="eddef-157">In the **Create new POM** window, accept the defaults and click **Finish**.</span></span>
3. <span data-ttu-id="eddef-158">Ga naar de **Projectverkenner** en open het bestand pom.xml.</span><span class="sxs-lookup"><span data-stu-id="eddef-158">In **Project Explorer**, open the pom.xml file.</span></span>
4. <span data-ttu-id="eddef-159">Klik op het tabblad **Dependencies** (Afhankelijkheden) van het deelvenster **Dependencies** (Afhankelijkheden) op **Add** (Toevoegen).</span><span class="sxs-lookup"><span data-stu-id="eddef-159">On the **Dependencies** tab, in the **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="eddef-160">Ga in het venster **Select Dependency** (Afhankelijkheid selecteren) als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="eddef-160">In the **Select Dependency** window, do the following:</span></span>
   
   * <span data-ttu-id="eddef-161">In de **groeps-Id** Voer com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="eddef-161">In the **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="eddef-162">In de **artefact-Id** Voer azure documentdb.</span><span class="sxs-lookup"><span data-stu-id="eddef-162">In the **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="eddef-163">In de **versie** Voer 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="eddef-163">In the **Version** box, enter 1.5.1.</span></span>
     
   ![DocumentDB Java Application SDK installeren](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="eddef-165">Of Voeg de afhankelijkheids-XML voor de groeps-Id en artefact-Id rechtstreeks aan pom.xml via een teksteditor:</span><span class="sxs-lookup"><span data-stu-id="eddef-165">Or add the dependency XML for Group Id and Artifact Id directly to the pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="eddef-166"><dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure documentdb</artifactId> <version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="eddef-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="eddef-167">Klik op **OK** en Maven de DocumentDB Java SDK installeert.</span><span class="sxs-lookup"><span data-stu-id="eddef-167">Click **OK** and Maven will install the DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="eddef-168">Sla het bestand pom.xml op.</span><span class="sxs-lookup"><span data-stu-id="eddef-168">Save the pom.xml file.</span></span>

## <span data-ttu-id="eddef-169"><a id="UseService"></a>Stap 4: de Azure Cosmos DB-service in een Java-toepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="eddef-169"><a id="UseService"></a>Step 4: Using the Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="eddef-170">Eerst laten we het object TodoItem definiëren in TodoItem.java:</span><span class="sxs-lookup"><span data-stu-id="eddef-170">First, let's define the TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="eddef-171">In dit project, gebruiken we [Project Lombok](http://projectlombok.org/) om de constructor, getters, setters en een opbouwfunctie te genereren.</span><span class="sxs-lookup"><span data-stu-id="eddef-171">In this project, we are using [Project Lombok](http://projectlombok.org/) to generate the constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="eddef-172">U kunt u deze code eventueel ook handmatig schrijven of door de IDE laten genereren.</span><span class="sxs-lookup"><span data-stu-id="eddef-172">Alternatively, you can write this code manually or have the IDE generate it.</span></span>
2. <span data-ttu-id="eddef-173">Als u de Azure Cosmos DB-service wilt aanroepen, moet u een nieuwe **DocumentClient** maken.</span><span class="sxs-lookup"><span data-stu-id="eddef-173">To invoke the Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="eddef-174">Doorgaans kunt u de **DocumentClient** het best opnieuw gebruiken, zodat u niet voor elke volgende aanvraag en nieuwe client hoeft te maken.</span><span class="sxs-lookup"><span data-stu-id="eddef-174">In general, it is best to reuse the **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="eddef-175">De client kan opnieuw worden gebruikt door deze in een **DocumentClientFactory** te verpakken.</span><span class="sxs-lookup"><span data-stu-id="eddef-175">We can reuse the client by wrapping the client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="eddef-176">In DocumentClientFactory.java, moet u de URI en primaire sleutel waarde die u hebt opgeslagen naar het Klembord in plakken [stap 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="eddef-176">In DocumentClientFactory.java, you need to paste the URI and PRIMARY KEY value you saved to your clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="eddef-177">Vervang [YOUR\_ENDPOINT\_HERE] door de URI en vervang [YOUR\_KEY\_HERE] door uw PRIMAIRE SLEUTEL.</span><span class="sxs-lookup"><span data-stu-id="eddef-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="eddef-178">U kunt nu een Data Access-object (DAO) maken om de ToDo-items naar Azure Cosmos DB te abstraheren.</span><span class="sxs-lookup"><span data-stu-id="eddef-178">Now let's create a Data Access Object (DAO) to abstract persisting our ToDo items to Azure Cosmos DB.</span></span>
   
    <span data-ttu-id="eddef-179">De client moet weten welke database en verzameling moeten worden gebruikt (waarnaar wordt verwezen via self link-elementen) om de ToDo-items op te kunnen slaan naar een verzameling.</span><span class="sxs-lookup"><span data-stu-id="eddef-179">In order to save ToDo items to a collection, the client needs to know which database and collection to persist to (as referenced by self-links).</span></span> <span data-ttu-id="eddef-180">Indien mogelijk slaat u de database en verzameling op in het cachegeheugen om extra retouren naar de database te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="eddef-180">In general, it is best to cache the database and collection when possible to avoid additional round-trips to the database.</span></span>
   
    <span data-ttu-id="eddef-181">De volgende code laat zien hoe u de database en verzameling ophaalt, indien de verzameling bestaat, of hoe u een nieuwe verzameling maakt als de verzameling niet bestaat:</span><span class="sxs-lookup"><span data-stu-id="eddef-181">The following code illustrates how to retrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // The name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // The name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // The Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for the database object, so we don't have to query for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for the collection object, so we don't have to query for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get the database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache the database object so we won't have to query for it
                        // later to retrieve the selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create the database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get the collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache the collection object so we won't have to query for it
                        // later to retrieve the selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create the collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - the app wasn't
                            // able to query or create the collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="eddef-182">Vervolgens moet u de code schrijven om de TodoItems door te geven naar de verzameling.</span><span class="sxs-lookup"><span data-stu-id="eddef-182">The next step is to write some code to persist the TodoItems in to the collection.</span></span> <span data-ttu-id="eddef-183">In dit voorbeeld gebruiken we [Gson](https://code.google.com/p/google-gson/) om TodoItem POJO's (Plain Old Java Objects) naar JSON-documenten te serialiseren en te deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="eddef-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) to serialize and de-serialize TodoItem Plain Old Java Objects (POJOs) to JSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize the TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate the document as a TodoItem for retrieval (so that we can
            // store multiple entity types in the collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist the document using the DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="eddef-184">De verwijzing naar documenten vindt net als bij Azure Cosmos DB-databases en -verzamelingen plaats via self link-elementen.</span><span class="sxs-lookup"><span data-stu-id="eddef-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="eddef-185">Met de volgende Help-functie kunt u documenten ophalen met een ander kenmerk (bijvoorbeeld 'id') in plaats van een self link-element:</span><span class="sxs-lookup"><span data-stu-id="eddef-185">The following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve the document using the DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. <span data-ttu-id="eddef-186">We kunnen de Help-methode in stap 5 gebruiken om een TodoItem JSON-document op te halen op basis van de id om het document vervolgens te deserialiseren naar een POJO:</span><span class="sxs-lookup"><span data-stu-id="eddef-186">We can use the helper method in step 5 to retrieve a TodoItem JSON document by id and then deserialize it to a POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve the document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize the document in to a TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="eddef-187">We kunnen ook de DocumentClient gebruiken om een verzameling of lijst met TodoItems op te halen met DocumentDB SQL:</span><span class="sxs-lookup"><span data-stu-id="eddef-187">We can also use the DocumentClient to get a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve the TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize the documents in to TodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="eddef-188">Er zijn verschillende manieren waarop een document kan worden bijgewerkt met de DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="eddef-188">There are many ways to update a document with the DocumentClient.</span></span> <span data-ttu-id="eddef-189">In onze takenlijsttoepassing moeten we kunnen aangeven of een TodoItem is voltooid of niet.</span><span class="sxs-lookup"><span data-stu-id="eddef-189">In our Todo list application, we want to be able to toggle whether a TodoItem is complete.</span></span> <span data-ttu-id="eddef-190">Dit kan worden gerealiseerd door het kenmerk 'complete' in het document bij te werken:</span><span class="sxs-lookup"><span data-stu-id="eddef-190">This can be achieved by updating the "complete" attribute within the document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve the document from the database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update the document as a JSON document directly.
            // For more complex operations - you could de-serialize the document in
            // to a POJO, update the POJO, and then re-serialize the POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace the updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="eddef-191">Tot slot willen we de mogelijkheid hebben om een TodoItem uit onze lijst te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="eddef-191">Finally, we want the ability to delete a TodoItem from our list.</span></span> <span data-ttu-id="eddef-192">Hiervoor kunnen we de eerder geschreven Help-methode gebruiken om het self link-element op te halen en de client vervolgens instrueren dat deze moet worden verwijderd:</span><span class="sxs-lookup"><span data-stu-id="eddef-192">To do this, we can use the helper method we wrote earlier to retrieve the self-link and then tell the client to delete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers to documents by self link rather than id.
   
            // Query for the document to retrieve the self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete the document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="eddef-193"><a id="Wire"></a>Stap 5: De rest van het project voor de ontwikkeling van een Java-toepassing aaneen koppelen</span><span class="sxs-lookup"><span data-stu-id="eddef-193"><a id="Wire"></a>Step 5: Wiring the rest of the of Java application development project together</span></span>
<span data-ttu-id="eddef-194">Nu dat we klaar bent met het leuk bits - alle die altijd ingeschakeld is voor een snelle gebruikersinterface maken en deze maximaal onze DAO.</span><span class="sxs-lookup"><span data-stu-id="eddef-194">Now that we've finished the fun bits - all that's left is to build a quick user interface and wire it up to our DAO.</span></span>

1. <span data-ttu-id="eddef-195">Laten we eerst een controller bouwen waarmee we onze DAO kunnen aanroepen:</span><span class="sxs-lookup"><span data-stu-id="eddef-195">First, let's start with building a controller to call our DAO:</span></span>
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    <span data-ttu-id="eddef-196">In complexere toepassing is het mogelijk dat de controller naast de DAO gecompliceerde bedrijfslogica bevat.</span><span class="sxs-lookup"><span data-stu-id="eddef-196">In a more complex application, the controller may house complicated business logic on top of the DAO.</span></span>
2. <span data-ttu-id="eddef-197">Vervolgens maken we een servlet om HTTP-aanvragen naar de controller te sturen:</span><span class="sxs-lookup"><span data-stu-id="eddef-197">Next, we'll create a servlet to route HTTP requests to the controller:</span></span>
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. <span data-ttu-id="eddef-198">We hebben een online gebruikersinterface weer te geven voor de gebruiker nodig.</span><span class="sxs-lookup"><span data-stu-id="eddef-198">We'll need a web user interface to display to the user.</span></span> <span data-ttu-id="eddef-199">Laten we het bestand index.jsp dat we eerder hebben gemaakt, herschrijven:</span><span class="sxs-lookup"><span data-stu-id="eddef-199">Let's re-write the index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding to body for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- The ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at the end of the document so the pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="eddef-200">En schrijf tot slot wat JavaScript aan de clientzijde om de online gebruikersinterface en de servlet met elkaar verbinden:</span><span class="sxs-lookup"><span data-stu-id="eddef-200">And finally, write some client-side JavaScript to tie the web user interface and the servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods to call Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api to update todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install the TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. <span data-ttu-id="eddef-201">Mooi.</span><span class="sxs-lookup"><span data-stu-id="eddef-201">Awesome!</span></span> <span data-ttu-id="eddef-202">Nu hoeft de toepassing alleen nog maar te worden getest.</span><span class="sxs-lookup"><span data-stu-id="eddef-202">Now all that's left is to test the application.</span></span> <span data-ttu-id="eddef-203">Voer de toepassing lokaal uit en voeg enkele Todo-items toe door de itemnaam en categorie in te vullen en op **Taak toevoegen** te klikken.</span><span class="sxs-lookup"><span data-stu-id="eddef-203">Run the application locally, and add some Todo items by filling in the item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="eddef-204">Zodra het item wordt weergegeven, kunt u bijwerken of het item is voltooid door het selectievakje in of uit te schakelen en op **Taken bijwerken** te klikken.</span><span class="sxs-lookup"><span data-stu-id="eddef-204">Once the item appears, you can update whether it's complete by toggling the checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="eddef-205"><a id="Deploy"></a>Stap 6: Implementeer uw Java-toepassing naar Azure websites</span><span class="sxs-lookup"><span data-stu-id="eddef-205"><a id="Deploy"></a>Step 6: Deploy your Java application to Azure Web Sites</span></span>
<span data-ttu-id="eddef-206">Azure websites kunt u net zo eenvoudig als uw toepassing wordt geëxporteerd als een WAR-bestand en uploaden via broncodebeheer (bijvoorbeeld Git) of FTP-Java-toepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="eddef-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="eddef-207">Als u wilt uw toepassing exporteren als een WAR-bestand, met de rechtermuisknop op het project in **Projectverkenner**, klikt u op **exporteren**, en klik vervolgens op **WAR-bestand**.</span><span class="sxs-lookup"><span data-stu-id="eddef-207">To export your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="eddef-208">Ga in het venster **WAR exporteren** als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="eddef-208">In the **WAR Export** window, do the following:</span></span>
   
   * <span data-ttu-id="eddef-209">Typ in het vak Webproject azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="eddef-209">In the Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="eddef-210">Kies in het vak Doel de bestemming waarnaar u het WAR-bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="eddef-210">In the Destination box, choose a destination to save the WAR file.</span></span>
   * <span data-ttu-id="eddef-211">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="eddef-211">Click **Finish**.</span></span>
3. <span data-ttu-id="eddef-212">Nu dat u een WAR-bestand in de hand hebt, kunt u gewoon uploaden naar uw Azure-website van **webapps** directory.</span><span class="sxs-lookup"><span data-stu-id="eddef-212">Now that you have a WAR file in hand, you can simply upload it to your Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="eddef-213">Zie voor instructies over het uploaden van het bestand [toevoegen van een Java-toepassing naar Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="eddef-213">For instructions on uploading the file, see [Add a Java application to Azure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="eddef-214">Zodra het WAR-bestand is geüpload naar de map webapps, detecteert de runtime-omgeving dat u het bestand hebt toegevoegd en wordt het bestand automatisch geladen.</span><span class="sxs-lookup"><span data-stu-id="eddef-214">Once the WAR file is uploaded to the webapps directory, the runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="eddef-215">Als u wilt het voltooide product weergeven, navigeert u naar http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ en start u uw taken toevoegt.</span><span class="sxs-lookup"><span data-stu-id="eddef-215">To view your finished product, navigate to http://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="eddef-216"><a id="GetProject"></a>Het project ophalen van GitHub</span><span class="sxs-lookup"><span data-stu-id="eddef-216"><a id="GetProject"></a>Get the project from GitHub</span></span>
<span data-ttu-id="eddef-217">Alle voorbeelden in deze zelfstudie zijn opgenomen in het [todo](https://github.com/Azure-Samples/documentdb-java-todo-app)-project op GitHub.</span><span class="sxs-lookup"><span data-stu-id="eddef-217">All the samples in this tutorial are included in the [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="eddef-218">Als u het todo-project wilt importeren in Eclipse, moet u over de software en resources beschikken die worden vermeld in de sectie [Vereisten](#Prerequisites) en gaat u als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="eddef-218">To import the todo project into Eclipse, ensure you have the software and resources listed in the [Prerequisites](#Prerequisites) section, then do the following:</span></span>

1. <span data-ttu-id="eddef-219">Installeer [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="eddef-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="eddef-220">Lombok wordt gebruikt om de constructors, getters, setters in het project te genereren.</span><span class="sxs-lookup"><span data-stu-id="eddef-220">Lombok is used to generate constructors, getters, setters in the project.</span></span> <span data-ttu-id="eddef-221">Zodra u het bestand lombok.jar hebt gedownload, dubbelklikt u op het bestand om het te installeren of installeert u het bestand vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="eddef-221">Once you have downloaded the lombok.jar file, double-click it to install it or install it from the command line.</span></span>
2. <span data-ttu-id="eddef-222">Als Eclipse is geopend, sluit en opent u Eclipse opnieuw om Lombok te laden.</span><span class="sxs-lookup"><span data-stu-id="eddef-222">If Eclipse is open, close it and restart it to load Lombok.</span></span>
3. <span data-ttu-id="eddef-223">Klik in Eclipse in het menu **File** (Bestand) op **Import** (Importeren).</span><span class="sxs-lookup"><span data-stu-id="eddef-223">In Eclipse, on the **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="eddef-224">Klik in het venster the **Import** (Importeren) achtereenvolgens op **Git**, **Projects from Git** (Projecten van Git) en **Next** (Volgende).</span><span class="sxs-lookup"><span data-stu-id="eddef-224">In the **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="eddef-225">Klik in het venster **Select Repository Source** (Opslagplaatsbron selecteren) op **Clone URI** (URI klonen).</span><span class="sxs-lookup"><span data-stu-id="eddef-225">On the **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="eddef-226">Op de **bron Git-opslagplaats** scherm in de **URI** vak en klik vervolgens op Voer https://github.com/Azure-Samples/java-todo-app.git **volgende**.</span><span class="sxs-lookup"><span data-stu-id="eddef-226">On the **Source Git Repository** screen, in the **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="eddef-227">Zorg er in het scherm **Branch Selection** (Vertakking selecteren) voor dat **master** is geselecteerd en klik op **Next** (Volgende).</span><span class="sxs-lookup"><span data-stu-id="eddef-227">On the **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="eddef-228">Klik in het scherm **Local Destination** (Lokale bestemming) op **Browse** (Bladeren) om een map te selecteren waarnaar de opslag kan worden gekopieerd en klik op **Next** (Volgende).</span><span class="sxs-lookup"><span data-stu-id="eddef-228">On the **Local Destination** screen, click **Browse** to select a folder where the repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="eddef-229">Zorg er in het scherm **Select a wizard to use for importing projects** (Een wizard selecteren waarmee projecten worden geïmporteerd) voor dat **Import existing projects** (Bestaande projecten selecteren) is geselecteerd en klik op **Next** (Volgende).</span><span class="sxs-lookup"><span data-stu-id="eddef-229">On the **Select a wizard to use for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="eddef-230">Schakel in het scherm **Import Projects** (Projecten importeren) het selectievakje uit voor het **DocumentDB-project** en klik op **Finish** (Voltooien).</span><span class="sxs-lookup"><span data-stu-id="eddef-230">On the **Import Projects** screen, unselect the **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="eddef-231">Het DocumentDB-project bevat de Azure Cosmos DB Java SDK, die we als een afhankelijkheid daarvan toevoegen zullen.</span><span class="sxs-lookup"><span data-stu-id="eddef-231">The DocumentDB project contains the Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="eddef-232">In **Projectverkenner**, gaat u naar Azure-documentdb-Java-sample\src\com.Microsoft.Azure.documentdb.sample.dao\DocumentClientFactory.Java en vervang de waarden voor HOST en MASTER_KEY door de URI en primaire sleutel voor uw Azure DB van de Cosmos-account en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="eddef-232">In **Project Explorer**, navigate to azure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace the HOST and MASTER_KEY values with the URI and PRIMARY KEY for your Azure Cosmos DB account, and then save the file.</span></span> <span data-ttu-id="eddef-233">Zie [Stap 1: Een Azure DB die Cosmos-databaseaccount maken](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="eddef-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="eddef-234">Klik in de **Projectverkenner** met de rechtermuisknop op **azure-documentdb-java-sample**, klik op **Build Path** (Opbouwpad) en klik vervolgens op **Configure Build Path** (Opbouwpad configureren).</span><span class="sxs-lookup"><span data-stu-id="eddef-234">In **Project Explorer**, right click the **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="eddef-235">Selecteer in het rechterdeelvenster van het scherm **Java Build Path** (Java-opbouwpad) het tabblad **Libraries** (Bibliotheken) en klik vervolgens op **Add External JARs** (Externe JAR's toevoegen).</span><span class="sxs-lookup"><span data-stu-id="eddef-235">On the **Java Build Path** screen, in the right pane, select the **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="eddef-236">Navigeer naar de locatie van het bestand lombok.jar en klik op **Open** (Openen) en **OK**.</span><span class="sxs-lookup"><span data-stu-id="eddef-236">Navigate to the location of the lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="eddef-237">Gebruik stap 12 om het venster **Properties** (Eigenschappen) opnieuw te openen en klik in het linkerdeelvenster vervolgens op **Targeted Runtimes** (Beoogde runtimes).</span><span class="sxs-lookup"><span data-stu-id="eddef-237">Use step 12 to open the **Properties** window again, and then in the left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="eddef-238">Klik in het scherm **Targeted Runtimes** (Beoogde runtimes) op **New** (Nieuw), selecteer **Apache Tomcat v7.0** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="eddef-238">On the **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="eddef-239">Gebruik stap 12 om het venster **Properties** (Eigenschappen) opnieuw te openen en klik in het linkerdeelvenster vervolgens op **Project Facets** (Projectfacetten).</span><span class="sxs-lookup"><span data-stu-id="eddef-239">Use step 12 to open the **Properties** window again, and then in the left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="eddef-240">Selecteer in het scherm **Project Facets** (Projectfacetten) achtereenvolgens **Dynamic Web Module** (Dynamische webmodule) en **Java** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="eddef-240">On the **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="eddef-241">Klik op het tabblad **Servers** onder aan het scherm met de rechtermuisknop op **Tomcat v7.0 Server at localhost** (Tomcat v7.0 Server op localhost) en klik vervolgens op **Add and Remove** (Toevoegen en verwijderen).</span><span class="sxs-lookup"><span data-stu-id="eddef-241">On the **Servers** tab at the bottom of the screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="eddef-242">Verplaats in het venster **Add and Remove** (Toevoegen en verwijderen) **azure-documentdb-java-sample** naar het vak **Configured** (Geconfigureerd) en klik vervolgens op **Finish** (Voltooien).</span><span class="sxs-lookup"><span data-stu-id="eddef-242">On the **Add and Remove** window, move **azure-documentdb-java-sample** to the **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="eddef-243">In de **Servers** tabblad, met de rechtermuisknop op **Tomcat v7.0 Server op localhost**, en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="eddef-243">In the **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="eddef-244">Navigeer in een browser naar http://localhost:8080/azure-documentdb-java-sample/ om taken aan uw takenlijst toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="eddef-244">In a browser, navigate to http://localhost:8080/azure-documentdb-java-sample/ and start adding to your task list.</span></span> <span data-ttu-id="eddef-245">Als u de standaardpoortwaarden hebt gewijzigd, wijzigt u 8080 in de waarde die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="eddef-245">Note that if you changed your default port values, change 8080 to the value you selected.</span></span>
22. <span data-ttu-id="eddef-246">Zie [Stap 6: Implementeren van uw toepassing naar Azure websites](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="eddef-246">To deploy your project to an Azure web site, see [Step 6. Deploy your application to Azure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
