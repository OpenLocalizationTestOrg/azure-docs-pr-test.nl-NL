---
title: aaaJava toepassing zelfstudie over het ontwikkelen met behulp van Azure DB die Cosmos | Microsoft Docs
description: Deze zelfstudie over Java-webtoepassingen ziet u hoe toouse hello Azure Cosmos DB en DocumentDB API toostore Hallo en toegang tot gegevens van een Java-toepassing gehost op Azure Websites.
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
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a><span data-ttu-id="2ed21-104">Een Java-webtoepassing met behulp van Azure DB die Cosmos en Hallo API DocumentDB bouwen</span><span class="sxs-lookup"><span data-stu-id="2ed21-104">Build a Java web application using Azure Cosmos DB and hello DocumentDB API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2ed21-105">.NET</span><span class="sxs-lookup"><span data-stu-id="2ed21-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="2ed21-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="2ed21-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="2ed21-107">Java</span><span class="sxs-lookup"><span data-stu-id="2ed21-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="2ed21-108">Python</span><span class="sxs-lookup"><span data-stu-id="2ed21-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="2ed21-109">Deze zelfstudie over Java-webtoepassingen ziet u hoe toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore en toegang tot gegevens van een Java-toepassing die worden gehost op Azure App Service Web Apps.</span><span class="sxs-lookup"><span data-stu-id="2ed21-109">This Java web application tutorial shows you how toouse hello [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service toostore and access data from a Java application hosted on Azure App Service Web Apps.</span></span> <span data-ttu-id="2ed21-110">In dit onderwerp leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="2ed21-110">In this topic, you will learn:</span></span>

* <span data-ttu-id="2ed21-111">Hoe toobuild een eenvoudige toepassing Java Server Pages (JSP) in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2ed21-111">How toobuild a basic JavaServer Pages (JSP) application in Eclipse.</span></span>
* <span data-ttu-id="2ed21-112">Hoe toowork Hello Azure Cosmos DB service met behulp van Hallo [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span><span class="sxs-lookup"><span data-stu-id="2ed21-112">How toowork with hello Azure Cosmos DB service using hello [Azure Cosmos DB Java SDK](https://github.com/Azure/azure-documentdb-java).</span></span>

<span data-ttu-id="2ed21-113">Deze zelfstudie over Java-toepassing ziet u hoe taken van taak-management-toepassing voor een webgebaseerde toocreate waarmee u toocreate, ophalen en markeren als voltooid is, zoals wordt weergegeven in Hallo volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="2ed21-113">This Java application tutorial shows you how toocreate a web-based task-management application that enables you toocreate, retrieve, and mark tasks as complete, as shown in hello following image.</span></span> <span data-ttu-id="2ed21-114">Hallo-taken in de takenlijst Hallo worden opgeslagen als JSON-documenten in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ed21-114">Each of hello tasks in hello ToDo list are stored as JSON documents in Azure Cosmos DB.</span></span>

![De Java-toepassing My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> <span data-ttu-id="2ed21-116">In deze zelfstudie voor het ontwikkelen van toepassingen wordt ervan uitgegaan dat u ervaring met Java hebt.</span><span class="sxs-lookup"><span data-stu-id="2ed21-116">This application development tutorial assumes that you have prior experience using Java.</span></span> <span data-ttu-id="2ed21-117">Als u nieuwe tooJava of Hallo [vereiste hulpprogramma's](#Prerequisites), het is raadzaam downloaden voltooid Hallo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project van GitHub en bouwen met behulp van [Hallo instructies aan Hallo einde van dit artikel](#GetProject).</span><span class="sxs-lookup"><span data-stu-id="2ed21-117">If you are new tooJava or hello [prerequisite tools](#Prerequisites), we recommend downloading hello complete [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project from GitHub and building it using [hello instructions at hello end of this article](#GetProject).</span></span> <span data-ttu-id="2ed21-118">Zodra u klaar hebt, kunt u Hallo artikel toogain informatie over Hallo-code in de context van project Hallo Hallo bekijken.</span><span class="sxs-lookup"><span data-stu-id="2ed21-118">Once you have it built, you can review hello article toogain insight on hello code in hello context of hello project.</span></span>  
> 
> 

## <span data-ttu-id="2ed21-119"><a id="Prerequisites"></a>Vereisten voor deze zelfstudie over Java-webtoepassingen</span><span class="sxs-lookup"><span data-stu-id="2ed21-119"><a id="Prerequisites"></a>Prerequisites for this Java web application tutorial</span></span>
<span data-ttu-id="2ed21-120">Voordat u deze zelfstudie voor het ontwikkelen van toepassing, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="2ed21-120">Before you begin this application development tutorial, you must have hello following:</span></span>

* <span data-ttu-id="2ed21-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2ed21-121">An active Azure account.</span></span> <span data-ttu-id="2ed21-122">Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken.</span><span class="sxs-lookup"><span data-stu-id="2ed21-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2ed21-123">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="2ed21-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span>

    <span data-ttu-id="2ed21-124">OF</span><span class="sxs-lookup"><span data-stu-id="2ed21-124">OR</span></span>

    <span data-ttu-id="2ed21-125">Een lokale installatie van Hallo [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2ed21-125">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md).</span></span>
* <span data-ttu-id="2ed21-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="2ed21-126">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* [<span data-ttu-id="2ed21-127">Eclipse IDE voor Java EE-ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="2ed21-127">Eclipse IDE for Java EE Developers.</span></span>](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [<span data-ttu-id="2ed21-128">Een Azure-website met een Java runtime environment (bijvoorbeeld Tomcat of Jetty) is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="2ed21-128">An Azure Web Site with a Java runtime environment (e.g. Tomcat or Jetty) enabled.</span></span>](../app-service-web/web-sites-java-get-started.md)

<span data-ttu-id="2ed21-129">Als u deze hulpprogramma's voor Hallo eerst installeert, coreservlets.com biedt een overzicht van het installatieproces Hallo in Snel starten Hallo-sectie van hun [zelfstudie: TomCat7 installeren en gebruiken met Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) artikel.</span><span class="sxs-lookup"><span data-stu-id="2ed21-129">If you're installing these tools for hello first time, coreservlets.com provides a walk-through of hello installation process in hello Quick Start section of their [Tutorial: Installing TomCat7 and Using it with Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) article.</span></span>

## <span data-ttu-id="2ed21-130"><a id="CreateDB"></a>Stap 1: Een Azure DB die Cosmos-account maken</span><span class="sxs-lookup"><span data-stu-id="2ed21-130"><a id="CreateDB"></a>Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="2ed21-131">Begin met het maken van een Azure Cosmos DB-account.</span><span class="sxs-lookup"><span data-stu-id="2ed21-131">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="2ed21-132">Als u al een account hebt of als u Azure Cosmos DB Emulator Hallo voor deze zelfstudie, kunt u overslaan te[stap 2: de Java JSP-toepassing hello maken](#CreateJSP).</span><span class="sxs-lookup"><span data-stu-id="2ed21-132">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create hello Java JSP application](#CreateJSP).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="2ed21-133"><a id="CreateJSP"></a>Stap 2: De Java JSP-toepassing hello maken</span><span class="sxs-lookup"><span data-stu-id="2ed21-133"><a id="CreateJSP"></a>Step 2: Create hello Java JSP application</span></span>
<span data-ttu-id="2ed21-134">toocreate hello JSP-toepassing:</span><span class="sxs-lookup"><span data-stu-id="2ed21-134">toocreate hello JSP application:</span></span>

1. <span data-ttu-id="2ed21-135">Als eerste moet u een Java-project maken.</span><span class="sxs-lookup"><span data-stu-id="2ed21-135">First, we’ll start off by creating a Java project.</span></span> <span data-ttu-id="2ed21-136">Start Eclipse en klik achtereenvolgens op **File** (Bestand), **New** (Nieuw) en **Dynamic Web Project** (Dynamisch webproject).</span><span class="sxs-lookup"><span data-stu-id="2ed21-136">Start Eclipse, then click **File**, click **New**, and then click **Dynamic Web Project**.</span></span> <span data-ttu-id="2ed21-137">Als er geen **dynamisch webproject** wordt aangeduid als een beschikbare project, Hallo te volgen: klik op **bestand**, klikt u op **nieuw**, klikt u op **Project**..., vouw **Web**, klikt u op **dynamisch webproject**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-137">If you don’t see **Dynamic Web Project** listed as an available project, do hello following: click **File**, click **New**, click **Project**…, expand **Web**, click **Dynamic Web Project**, and click **Next**.</span></span>
   
    ![JSP Java-toepassing ontwikkelen](./media/documentdb-java-application/image10.png)
2. <span data-ttu-id="2ed21-139">Voer een projectnaam in Hallo **projectnaam** vak en in Hallo **Doelruntime** vervolgkeuzelijst, selecteer desgewenst een waarde (bijvoorbeeld Apache Tomcat v7.0) en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-139">Enter a project name in hello **Project name** box, and in hello **Target Runtime** drop-down menu, optionally select a value (e.g. Apache Tomcat v7.0), and then click **Finish**.</span></span> <span data-ttu-id="2ed21-140">Een doelruntime te selecteren, kunt u toorun uw project lokaal via Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2ed21-140">Selecting a target runtime enables you toorun your project locally through Eclipse.</span></span>
3. <span data-ttu-id="2ed21-141">Vouw in de weergave Project Explorer Hallo in Eclipse uw project.</span><span class="sxs-lookup"><span data-stu-id="2ed21-141">In Eclipse, in hello Project Explorer view, expand your project.</span></span> <span data-ttu-id="2ed21-142">Klik met de rechtermuisknop op **WebContent**(Webinhoud) en klik vervolgens op **New** (Nieuw) en **JSP File** (JSP-bestand).</span><span class="sxs-lookup"><span data-stu-id="2ed21-142">Right-click **WebContent**, click **New**, and then click **JSP File**.</span></span>
4. <span data-ttu-id="2ed21-143">In Hallo **nieuw JSP-bestand** in het dialoogvenster, naam Hallo bestand **index.jsp**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-143">In hello **New JSP File** dialog box, name hello file **index.jsp**.</span></span> <span data-ttu-id="2ed21-144">Hallo bovenliggende map als houden **WebContent**, zoals weergegeven in Hallo van de volgende afbeelding en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-144">Keep hello parent folder as **WebContent**, as shown in hello following illustration, and then click **Next**.</span></span>
   
    ![Een nieuw JSP-bestand maken - Zelfstudie Java-webtoepassing](./media/documentdb-java-application/image11.png)
5. <span data-ttu-id="2ed21-146">In Hallo **JSP-sjabloon selecteren** in het dialoogvenster voor doel van deze zelfstudie select Hallo **nieuw JSP-bestand (html)**, en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-146">In hello **Select JSP Template** dialog box, for hello purpose of this tutorial select **New JSP File (html)**, and then click **Finish**.</span></span>
6. <span data-ttu-id="2ed21-147">Wanneer Hallo index.jsp bestand wordt geopend in Eclipse, voegt u tekst toodisplay **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="2ed21-147">When hello index.jsp file opens in Eclipse, add text toodisplay **Hello World!**</span></span> <span data-ttu-id="2ed21-148">binnen de bestaande Hallo <body> element.</span><span class="sxs-lookup"><span data-stu-id="2ed21-148">within hello existing <body> element.</span></span> <span data-ttu-id="2ed21-149">Uw bijgewerkte <body> inhoud moet eruitzien als Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ed21-149">Your updated <body> content should look like hello following code:</span></span>
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. <span data-ttu-id="2ed21-150">Hallo index.jsp bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="2ed21-150">Save hello index.jsp file.</span></span>
8. <span data-ttu-id="2ed21-151">Als u een doelruntime in stap 2 hebt ingesteld, kunt u **Project** en vervolgens **uitvoeren** toorun uw JSP-toepassing lokaal:</span><span class="sxs-lookup"><span data-stu-id="2ed21-151">If you set a target runtime in step 2, you can click **Project** and then **Run** toorun your JSP application locally:</span></span>
   
    ![Hello World – Zelfstudie Java-toepassing](./media/documentdb-java-application/image12.png)

## <span data-ttu-id="2ed21-153"><a id="InstallSDK"></a>Stap 3: Hallo DocumentDB Java SDK installeren</span><span class="sxs-lookup"><span data-stu-id="2ed21-153"><a id="InstallSDK"></a>Step 3: Install hello DocumentDB Java SDK</span></span>
<span data-ttu-id="2ed21-154">Hallo gemakkelijkste manier toopull in Hallo DocumentDB Java SDK en de bijbehorende afhankelijkheden is via [Apache Maven](http://maven.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="2ed21-154">hello easiest way toopull in hello DocumentDB Java SDK and its dependencies is through [Apache Maven](http://maven.apache.org/).</span></span>

<span data-ttu-id="2ed21-155">toodo, moet u tooconvert uw project tooa maven-project door Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="2ed21-155">toodo this, you will need tooconvert your project tooa maven project by completing hello following steps:</span></span>

1. <span data-ttu-id="2ed21-156">Met de rechtermuisknop op het project in Hallo Projectverkenner, klikt u op **configureren**, klikt u op **tooMaven Project converteren**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-156">Right-click your project in hello Project Explorer, click **Configure**, click **Convert tooMaven Project**.</span></span>
2. <span data-ttu-id="2ed21-157">In Hallo **nieuwe POM maken** venster Hallo standaardinstellingen accepteren en op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-157">In hello **Create new POM** window, accept hello defaults and click **Finish**.</span></span>
3. <span data-ttu-id="2ed21-158">In **Projectverkenner**Open Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="2ed21-158">In **Project Explorer**, open hello pom.xml file.</span></span>
4. <span data-ttu-id="2ed21-159">Op Hallo **afhankelijkheden** tabblad in Hallo **afhankelijkheden** deelvenster, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-159">On hello **Dependencies** tab, in hello **Dependencies** pane, click **Add**.</span></span>
5. <span data-ttu-id="2ed21-160">In Hallo **afhankelijkheid selecteren** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ed21-160">In hello **Select Dependency** window, do hello following:</span></span>
   
   * <span data-ttu-id="2ed21-161">In Hallo **groeps-Id** Voer com.microsoft.azure.</span><span class="sxs-lookup"><span data-stu-id="2ed21-161">In hello **Group Id** box, enter com.microsoft.azure.</span></span>
   * <span data-ttu-id="2ed21-162">In Hallo **artefact-Id** Voer azure documentdb.</span><span class="sxs-lookup"><span data-stu-id="2ed21-162">In hello **Artifact Id** box, enter azure-documentdb.</span></span>
   * <span data-ttu-id="2ed21-163">In Hallo **versie** Voer 1.5.1.</span><span class="sxs-lookup"><span data-stu-id="2ed21-163">In hello **Version** box, enter 1.5.1.</span></span>
     
   ![DocumentDB Java Application SDK installeren](./media/documentdb-java-application/image13.png)
     
   * <span data-ttu-id="2ed21-165">Of voeg Hallo afhankelijkheids-XML voor de groeps-Id en artefact-Id rechtstreeks toohello pom.xml via een teksteditor:</span><span class="sxs-lookup"><span data-stu-id="2ed21-165">Or add hello dependency XML for Group Id and Artifact Id directly toohello pom.xml via a text editor:</span></span>
     
        <span data-ttu-id="2ed21-166"><dependency><groupId>com.microsoft.azure</groupId> <artifactId>azure documentdb</artifactId> <version>1.9.1</version></dependency></span><span class="sxs-lookup"><span data-stu-id="2ed21-166"><dependency> <groupId>com.microsoft.azure</groupId> <artifactId>azure-documentdb</artifactId> <version>1.9.1</version> </dependency></span></span>
6. <span data-ttu-id="2ed21-167">Klik op **OK** en Maven hello DocumentDB Java SDK installeert.</span><span class="sxs-lookup"><span data-stu-id="2ed21-167">Click **OK** and Maven will install hello DocumentDB Java SDK.</span></span>
7. <span data-ttu-id="2ed21-168">Hallo pom.xml-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="2ed21-168">Save hello pom.xml file.</span></span>

## <span data-ttu-id="2ed21-169"><a id="UseService"></a>Stap 4: Gebruik hello Azure DB die Cosmos-service in een Java-toepassing</span><span class="sxs-lookup"><span data-stu-id="2ed21-169"><a id="UseService"></a>Step 4: Using hello Azure Cosmos DB service in a Java application</span></span>
1. <span data-ttu-id="2ed21-170">Eerst gaan we in TodoItem.java definiëren Hallo TodoItem object:</span><span class="sxs-lookup"><span data-stu-id="2ed21-170">First, let's define hello TodoItem object in TodoItem.java:</span></span>
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    <span data-ttu-id="2ed21-171">In dit project, gebruiken we [Project Lombok](http://projectlombok.org/) toogenerate Hallo constructor, getters, setters en een opbouwfunctie.</span><span class="sxs-lookup"><span data-stu-id="2ed21-171">In this project, we are using [Project Lombok](http://projectlombok.org/) toogenerate hello constructor, getters, setters, and a builder.</span></span> <span data-ttu-id="2ed21-172">U kunt ook handmatig schrijven van deze code of hebben Hallo IDE gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="2ed21-172">Alternatively, you can write this code manually or have hello IDE generate it.</span></span>
2. <span data-ttu-id="2ed21-173">tooinvoke hello Azure DB die Cosmos-service, moet u instantiëren een nieuwe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-173">tooinvoke hello Azure Cosmos DB service, you must instantiate a new **DocumentClient**.</span></span> <span data-ttu-id="2ed21-174">In het algemeen is het beste tooreuse hello **DocumentClient** - in plaats van te maken van een nieuwe client voor elke volgende aanvraag.</span><span class="sxs-lookup"><span data-stu-id="2ed21-174">In general, it is best tooreuse hello **DocumentClient** - rather than construct a new client for each subsequent request.</span></span> <span data-ttu-id="2ed21-175">Hallo-client kan worden hergebruikt door Hallo-client in een **DocumentClientFactory**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-175">We can reuse hello client by wrapping hello client in a **DocumentClientFactory**.</span></span> <span data-ttu-id="2ed21-176">In de DocumentClientFactory.java, moet u toopaste Hallo URI en primaire sleutel waarde opgeslagen van Klembord in tooyour [stap 1](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="2ed21-176">In DocumentClientFactory.java, you need toopaste hello URI and PRIMARY KEY value you saved tooyour clipboard in [step 1](#CreateDB).</span></span> <span data-ttu-id="2ed21-177">Vervang [YOUR\_ENDPOINT\_HERE] door de URI en vervang [YOUR\_KEY\_HERE] door uw PRIMAIRE SLEUTEL.</span><span class="sxs-lookup"><span data-stu-id="2ed21-177">Replace [YOUR\_ENDPOINT\_HERE] with your URI and replace [YOUR\_KEY\_HERE] with your PRIMARY KEY.</span></span>
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. <span data-ttu-id="2ed21-178">Nu gaan we maken een Data Access-Object (DAO) tooabstract behouden blijven van onze ToDo-items tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2ed21-178">Now let's create a Data Access Object (DAO) tooabstract persisting our ToDo items tooAzure Cosmos DB.</span></span>
   
    <span data-ttu-id="2ed21-179">In volgorde toosave ToDo-items tooa verzameling, Hallo client moet tooknow welke database en verzameling toopersist te (waarnaar wordt verwezen via Self link-elementen).</span><span class="sxs-lookup"><span data-stu-id="2ed21-179">In order toosave ToDo items tooa collection, hello client needs tooknow which database and collection toopersist too(as referenced by self-links).</span></span> <span data-ttu-id="2ed21-180">In het algemeen is het beste toocache Hallo-database en verzameling indien mogelijk tooavoid extra retouren toohello database.</span><span class="sxs-lookup"><span data-stu-id="2ed21-180">In general, it is best toocache hello database and collection when possible tooavoid additional round-trips toohello database.</span></span>
   
    <span data-ttu-id="2ed21-181">Hallo volgende code laat zien hoe tooretrieve de database en verzameling, als deze bestaat, of een nieuwe maken als deze niet bestaat:</span><span class="sxs-lookup"><span data-stu-id="2ed21-181">hello following code illustrates how tooretrieve our database and collection, if it exists, or create a new one if it doesn't exist:</span></span>
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. <span data-ttu-id="2ed21-182">de volgende stap Hallo toowrite sommige code toopersist Hallo taken in de verzameling toohello is.</span><span class="sxs-lookup"><span data-stu-id="2ed21-182">hello next step is toowrite some code toopersist hello TodoItems in toohello collection.</span></span> <span data-ttu-id="2ed21-183">In dit voorbeeld gebruiken we [Gson](https://code.google.com/p/google-gson/) tooserialize en TodoItem Plain Old Java Objects (pojo's) tooJSON documenten niet deserialiseren.</span><span class="sxs-lookup"><span data-stu-id="2ed21-183">In this example, we will use [Gson](https://code.google.com/p/google-gson/) tooserialize and de-serialize TodoItem Plain Old Java Objects (POJOs) tooJSON documents.</span></span>
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. <span data-ttu-id="2ed21-184">De verwijzing naar documenten vindt net als bij Azure Cosmos DB-databases en -verzamelingen plaats via self link-elementen.</span><span class="sxs-lookup"><span data-stu-id="2ed21-184">Like Azure Cosmos DB databases and collections, documents are also referenced by self-links.</span></span> <span data-ttu-id="2ed21-185">Hallo volgende Help-functie kunt ons documenten ophalen door een ander kenmerk (bijvoorbeeld ' id') in plaats van self link-element:</span><span class="sxs-lookup"><span data-stu-id="2ed21-185">hello following helper function lets us retrieve documents by another attribute (e.g. "id") rather than self-link:</span></span>
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
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
6. <span data-ttu-id="2ed21-186">We kunnen Hallo Help-methode in stap 5 tooretrieve een TodoItem JSON-document gebruiken door-id en vervolgens te deserialiseren tooa POJO:</span><span class="sxs-lookup"><span data-stu-id="2ed21-186">We can use hello helper method in step 5 tooretrieve a TodoItem JSON document by id and then deserialize it tooa POJO:</span></span>
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. <span data-ttu-id="2ed21-187">We kunnen ook Hallo DocumentClient tooget gebruiken een verzameling of lijst met TodoItems met DocumentDB SQL:</span><span class="sxs-lookup"><span data-stu-id="2ed21-187">We can also use hello DocumentClient tooget a collection or list of TodoItems using DocumentDB SQL:</span></span>
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. <span data-ttu-id="2ed21-188">Er zijn veel manieren tooupdate een document met Hallo DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="2ed21-188">There are many ways tooupdate a document with hello DocumentClient.</span></span> <span data-ttu-id="2ed21-189">In onze takenlijsttoepassing willen we toobe kunnen tootoggle of een TodoItem voltooid is.</span><span class="sxs-lookup"><span data-stu-id="2ed21-189">In our Todo list application, we want toobe able tootoggle whether a TodoItem is complete.</span></span> <span data-ttu-id="2ed21-190">Dit kan worden gerealiseerd door 'complete' Hallo-kenmerk in Hallo document te werken:</span><span class="sxs-lookup"><span data-stu-id="2ed21-190">This can be achieved by updating hello "complete" attribute within hello document:</span></span>
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. <span data-ttu-id="2ed21-191">Tot slot willen we Hallo mogelijkheid toodelete een TodoItem uit onze lijst.</span><span class="sxs-lookup"><span data-stu-id="2ed21-191">Finally, we want hello ability toodelete a TodoItem from our list.</span></span> <span data-ttu-id="2ed21-192">toodo, kunnen we Hallo eerder geschreven Help-methode gebruiken tooretrieve Hallo Self link-element en vervolgens instrueren Hallo client toodelete het:</span><span class="sxs-lookup"><span data-stu-id="2ed21-192">toodo this, we can use hello helper method we wrote earlier tooretrieve hello self-link and then tell hello client toodelete it:</span></span>
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <span data-ttu-id="2ed21-193"><a id="Wire"></a>Stap 5: Rest Hallo van project voor de ontwikkeling van Java-toepassing hello samen bekabeling</span><span class="sxs-lookup"><span data-stu-id="2ed21-193"><a id="Wire"></a>Step 5: Wiring hello rest of hello of Java application development project together</span></span>
<span data-ttu-id="2ed21-194">Nu dat we klaar bent met het Hallo plezier bits - alle die altijd ingeschakeld toobuild is een snelle gebruikersinterface en deze up tooour DAO.</span><span class="sxs-lookup"><span data-stu-id="2ed21-194">Now that we've finished hello fun bits - all that's left is toobuild a quick user interface and wire it up tooour DAO.</span></span>

1. <span data-ttu-id="2ed21-195">Eerst laten we beginnen met het bouwen van een domeincontroller toocall onze DAO:</span><span class="sxs-lookup"><span data-stu-id="2ed21-195">First, let's start with building a controller toocall our DAO:</span></span>
   
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
   
    <span data-ttu-id="2ed21-196">Hallo controller mogelijk gecompliceerde bedrijfslogica boven op Hallo DAO dat in een complexere toepassing.</span><span class="sxs-lookup"><span data-stu-id="2ed21-196">In a more complex application, hello controller may house complicated business logic on top of hello DAO.</span></span>
2. <span data-ttu-id="2ed21-197">Vervolgens maken we een servlet tooroute HTTP-aanvragen toohello domeincontroller:</span><span class="sxs-lookup"><span data-stu-id="2ed21-197">Next, we'll create a servlet tooroute HTTP requests toohello controller:</span></span>
   
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
3. <span data-ttu-id="2ed21-198">We hebben een web user interface toodisplay toohello gebruiker nodig.</span><span class="sxs-lookup"><span data-stu-id="2ed21-198">We'll need a web user interface toodisplay toohello user.</span></span> <span data-ttu-id="2ed21-199">We gaan opnieuw schrijven Hallo index.jsp dat we eerder hebben gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2ed21-199">Let's re-write hello index.jsp we created earlier:</span></span>
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
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
   
            <!-- hello ToDo List -->
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
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. <span data-ttu-id="2ed21-200">Ten slotte schrijven sommige clientzijde JavaScript tootie Hallo online gebruikersinterface en Hallo servlet samen:</span><span class="sxs-lookup"><span data-stu-id="2ed21-200">And finally, write some client-side JavaScript tootie hello web user interface and hello servlet together:</span></span>
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
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
   
              // Call api tooupdate todo items.
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
           * Install hello TodoApp
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
5. <span data-ttu-id="2ed21-201">Mooi.</span><span class="sxs-lookup"><span data-stu-id="2ed21-201">Awesome!</span></span> <span data-ttu-id="2ed21-202">Alle die altijd ingeschakeld is nu tootest Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2ed21-202">Now all that's left is tootest hello application.</span></span> <span data-ttu-id="2ed21-203">Hallo-toepassing lokaal uitvoeren en enkele Todo-items toevoegen door te vullen Hallo itemnaam en categorie en te klikken op **taak toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-203">Run hello application locally, and add some Todo items by filling in hello item name and category and clicking **Add Task**.</span></span>
6. <span data-ttu-id="2ed21-204">Zodra het Hallo-item wordt weergegeven, kunt u bijwerken of deze voltooid is door Hallo selectievakje in te schakelen en te klikken op **taken bijwerken**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-204">Once hello item appears, you can update whether it's complete by toggling hello checkbox and clicking **Update Tasks**.</span></span>

## <span data-ttu-id="2ed21-205"><a id="Deploy"></a>Stap 6: De Java-toepassing tooAzure websites implementeren</span><span class="sxs-lookup"><span data-stu-id="2ed21-205"><a id="Deploy"></a>Step 6: Deploy your Java application tooAzure Web Sites</span></span>
<span data-ttu-id="2ed21-206">Azure websites kunt u net zo eenvoudig als uw toepassing wordt geëxporteerd als een WAR-bestand en uploaden via broncodebeheer (bijvoorbeeld Git) of FTP-Java-toepassingen implementeren.</span><span class="sxs-lookup"><span data-stu-id="2ed21-206">Azure Web Sites makes deploying Java applications as simple as exporting your application as a WAR file and either uploading it via source control (e.g. Git) or FTP.</span></span>

1. <span data-ttu-id="2ed21-207">tooexport uw toepassing als een WAR-bestand met de rechtermuisknop op het project in **Projectverkenner**, klikt u op **exporteren**, en klik vervolgens op **WAR-bestand**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-207">tooexport your application as a WAR file, right-click on your project in **Project Explorer**, click **Export**, and then click **WAR File**.</span></span>
2. <span data-ttu-id="2ed21-208">In Hallo **WAR exporteren** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ed21-208">In hello **WAR Export** window, do hello following:</span></span>
   
   * <span data-ttu-id="2ed21-209">Voer in Hallo vak webproject azure-documentdb-java-sample.</span><span class="sxs-lookup"><span data-stu-id="2ed21-209">In hello Web project box, enter azure-documentdb-java-sample.</span></span>
   * <span data-ttu-id="2ed21-210">Kies een doel toosave Hallo WAR-bestand in Hallo doellocatie.</span><span class="sxs-lookup"><span data-stu-id="2ed21-210">In hello Destination box, choose a destination toosave hello WAR file.</span></span>
   * <span data-ttu-id="2ed21-211">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-211">Click **Finish**.</span></span>
3. <span data-ttu-id="2ed21-212">Nu dat u een WAR-bestand in de hand hebt, kunt u gewoon uploaden tooyour Azure-website van **webapps** directory.</span><span class="sxs-lookup"><span data-stu-id="2ed21-212">Now that you have a WAR file in hand, you can simply upload it tooyour Azure Web Site's **webapps** directory.</span></span> <span data-ttu-id="2ed21-213">Zie voor instructies over het Hallo-bestand uploaden [toevoegen van een Java-toepassing tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span><span class="sxs-lookup"><span data-stu-id="2ed21-213">For instructions on uploading hello file, see [Add a Java application tooAzure App Service Web Apps](../app-service-web/web-sites-java-add-app.md).</span></span>
   
    <span data-ttu-id="2ed21-214">Zodra het Hallo WAR-bestand is geüpload toohello map WebApps, detecteert Hallo runtime-omgeving dat u deze hebt toegevoegd en wordt automatisch geladen.</span><span class="sxs-lookup"><span data-stu-id="2ed21-214">Once hello WAR file is uploaded toohello webapps directory, hello runtime environment will detect that you've added it and will automatically load it.</span></span>
4. <span data-ttu-id="2ed21-215">tooview het voltooide product Navigeer toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ en start u uw taken toevoegt.</span><span class="sxs-lookup"><span data-stu-id="2ed21-215">tooview your finished product, navigate toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ and start adding your tasks!</span></span>

## <span data-ttu-id="2ed21-216"><a id="GetProject"></a>Hallo-project ophalen van GitHub</span><span class="sxs-lookup"><span data-stu-id="2ed21-216"><a id="GetProject"></a>Get hello project from GitHub</span></span>
<span data-ttu-id="2ed21-217">Alle Hallo voorbeelden in deze zelfstudie zijn opgenomen in Hallo [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project op GitHub.</span><span class="sxs-lookup"><span data-stu-id="2ed21-217">All hello samples in this tutorial are included in hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) project on GitHub.</span></span> <span data-ttu-id="2ed21-218">tooimport hello todo-project in Eclipse, Controleer of u hebt Hallo software en bronnen in Hallo [vereisten](#Prerequisites) sectie vervolgens Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="2ed21-218">tooimport hello todo project into Eclipse, ensure you have hello software and resources listed in hello [Prerequisites](#Prerequisites) section, then do hello following:</span></span>

1. <span data-ttu-id="2ed21-219">Installeer [Project Lombok](http://projectlombok.org/).</span><span class="sxs-lookup"><span data-stu-id="2ed21-219">Install [Project Lombok](http://projectlombok.org/).</span></span> <span data-ttu-id="2ed21-220">Lombok is gebruikte toogenerate constructors, getters, setters in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="2ed21-220">Lombok is used toogenerate constructors, getters, setters in hello project.</span></span> <span data-ttu-id="2ed21-221">Zodra u Hallo lombok.jar bestand hebt gedownload, dubbelklikt u op het tooinstall het of installeren vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2ed21-221">Once you have downloaded hello lombok.jar file, double-click it tooinstall it or install it from hello command line.</span></span>
2. <span data-ttu-id="2ed21-222">Als Eclipse geopend is, sluit en opnieuw tooload Lombok.</span><span class="sxs-lookup"><span data-stu-id="2ed21-222">If Eclipse is open, close it and restart it tooload Lombok.</span></span>
3. <span data-ttu-id="2ed21-223">In Eclipse op Hallo **bestand** menu, klikt u op **importeren**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-223">In Eclipse, on hello **File** menu, click **Import**.</span></span>
4. <span data-ttu-id="2ed21-224">In Hallo **importeren** venster, klikt u op **Git**, klikt u op **projecten van Git**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-224">In hello **Import** window, click **Git**, click **Projects from Git**, and then click **Next**.</span></span>
5. <span data-ttu-id="2ed21-225">Op Hallo **opslagplaats bron selecteren** scherm, klikt u op **Clone URI**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-225">On hello **Select Repository Source** screen, click **Clone URI**.</span></span>
6. <span data-ttu-id="2ed21-226">Op Hallo **bron Git-opslagplaats** scherm in Hallo **URI** vak en klik vervolgens op Voer https://github.com/Azure-Samples/java-todo-app.git **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-226">On hello **Source Git Repository** screen, in hello **URI** box, enter https://github.com/Azure-Samples/java-todo-app.git, and then click **Next**.</span></span>
7. <span data-ttu-id="2ed21-227">Op Hallo **vertakking selectie** scherm **master** is geselecteerd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-227">On hello **Branch Selection** screen, ensure that **master** is selected, and then click **Next**.</span></span>
8. <span data-ttu-id="2ed21-228">Op Hallo **lokale bestemming** scherm, klikt u op **Bladeren** tooselect een map waar de Hallo opslagplaats kunnen worden gekopieerd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-228">On hello **Local Destination** screen, click **Browse** tooselect a folder where hello repository can be copied, and then click **Next**.</span></span>
9. <span data-ttu-id="2ed21-229">Op Hallo **een toouse wizard voor het importeren van de projecten selecteren** scherm **bestaande projecten importeren** is geselecteerd en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-229">On hello **Select a wizard toouse for importing projects** screen, ensure that **Import existing projects** is selected, and then click **Next**.</span></span>
10. <span data-ttu-id="2ed21-230">Op Hallo **importeren projecten** scherm, opheffen Hallo **DocumentDB** project en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-230">On hello **Import Projects** screen, unselect hello **DocumentDB** project, and then click **Finish**.</span></span> <span data-ttu-id="2ed21-231">Hallo DocumentDB-project bevat hello Azure Cosmos DB Java SDK, die we als een afhankelijkheid daarvan toevoegen zullen.</span><span class="sxs-lookup"><span data-stu-id="2ed21-231">hello DocumentDB project contains hello Azure Cosmos DB Java SDK, which we will add as a dependency instead.</span></span>
11. <span data-ttu-id="2ed21-232">In **Projectverkenner**, gaat u tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java en Hallo HOST en MASTER_KEY waarden vervangt door Hallo URI en primaire sleutel voor uw Azure DB die Cosmos-account en vervolgens opgeslagen Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="2ed21-232">In **Project Explorer**, navigate tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java and replace hello HOST and MASTER_KEY values with hello URI and PRIMARY KEY for your Azure Cosmos DB account, and then save hello file.</span></span> <span data-ttu-id="2ed21-233">Zie [Stap 1: Een Azure DB die Cosmos-databaseaccount maken](#CreateDB).</span><span class="sxs-lookup"><span data-stu-id="2ed21-233">For more information, see [Step 1. Create an Azure Cosmos DB database account](#CreateDB).</span></span>
12. <span data-ttu-id="2ed21-234">In **Projectverkenner**, klik met de rechtermuisknop op Hallo **azure-documentdb-java-sample**, klikt u op **pad**, en klik vervolgens op **configureren pad**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-234">In **Project Explorer**, right click hello **azure-documentdb-java-sample**, click **Build Path**, and then click **Configure Build Path**.</span></span>
13. <span data-ttu-id="2ed21-235">Op Hallo **Javabuild-pad** in het rechterdeelvenster hello, selecteer Hallo scherm **bibliotheken** tabblad en klik vervolgens op **externe JARs toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-235">On hello **Java Build Path** screen, in hello right pane, select hello **Libraries** tab, and then click **Add External JARs**.</span></span> <span data-ttu-id="2ed21-236">Navigeer toohello locatie van Hallo lombok.jar bestand en klik op **Open**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-236">Navigate toohello location of hello lombok.jar file, and click **Open**, and then click **OK**.</span></span>
14. <span data-ttu-id="2ed21-237">Gebruik stap 12 tooopen hello **eigenschappen** venster opnieuw, en klik in het linkerdeelvenster Hallo vervolgens op **Runtimes gericht**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-237">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Targeted Runtimes**.</span></span>
15. <span data-ttu-id="2ed21-238">Op Hallo **Runtimes gericht** scherm, klikt u op **nieuw**, selecteer **Apache Tomcat v7.0**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-238">On hello **Targeted Runtimes** screen, click **New**, select **Apache Tomcat v7.0**, and then click **OK**.</span></span>
16. <span data-ttu-id="2ed21-239">Gebruik stap 12 tooopen hello **eigenschappen** venster opnieuw, en klik in het linkerdeelvenster Hallo vervolgens op **Project-facetten**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-239">Use step 12 tooopen hello **Properties** window again, and then in hello left pane click **Project Facets**.</span></span>
17. <span data-ttu-id="2ed21-240">Op Hallo **Project-facetten** Schakel in het scherm **Dynamic Web Module** en **Java**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-240">On hello **Project Facets** screen, select **Dynamic Web Module** and **Java**, and then click **OK**.</span></span>
18. <span data-ttu-id="2ed21-241">Op Hallo **Servers** tabblad Hallo welkomstscherm onderaan in, met de rechtermuisknop op **Tomcat v7.0 Server op localhost** en klik vervolgens op **toevoegen en verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-241">On hello **Servers** tab at hello bottom of hello screen, right-click **Tomcat v7.0 Server at localhost** and then click **Add and Remove**.</span></span>
19. <span data-ttu-id="2ed21-242">Op Hallo **toevoegen en verwijderen** venster verplaatsen **azure-documentdb-java-sample** toohello **geconfigureerde** vak en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-242">On hello **Add and Remove** window, move **azure-documentdb-java-sample** toohello **Configured** box, and then click **Finish**.</span></span>
20. <span data-ttu-id="2ed21-243">In Hallo **Servers** tabblad, met de rechtermuisknop op **Tomcat v7.0 Server op localhost**, en klik vervolgens op **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="2ed21-243">In hello **Servers** tab, right-click **Tomcat v7.0 Server at localhost**, and then click **Restart**.</span></span>
21. <span data-ttu-id="2ed21-244">Navigeer in een browser toohttp://localhost:8080 / azure-documentdb-java-sample / toe te voegen tooyour takenlijst.</span><span class="sxs-lookup"><span data-stu-id="2ed21-244">In a browser, navigate toohttp://localhost:8080/azure-documentdb-java-sample/ and start adding tooyour task list.</span></span> <span data-ttu-id="2ed21-245">Let op: als u standaardpoortwaarden, wijzigt u 8080 toohello waarde die u geselecteerd wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2ed21-245">Note that if you changed your default port values, change 8080 toohello value you selected.</span></span>
22. <span data-ttu-id="2ed21-246">toodeploy uw project tooan Azure-website, Zie [stap 6. Implementeren van uw toepassing tooAzure websites](#Deploy).</span><span class="sxs-lookup"><span data-stu-id="2ed21-246">toodeploy your project tooan Azure web site, see [Step 6. Deploy your application tooAzure Web Sites](#Deploy).</span></span>

[1]: media/documentdb-java-application/keys.png
