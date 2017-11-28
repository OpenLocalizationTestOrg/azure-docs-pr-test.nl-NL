---
title: Het gebruik van de opstartinstallatiekopie Spring Starter met een Azure-API voor DocumentDB Cosmos DB
description: Informatie over het configureren van een toepassing die is gemaakt met de versie die voorjaar opstarten initialisatiefunctie met de Azure-API voor DocumentDB Cosmos DB.
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring opstarten Starter Cosmos DB
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: 273cc750857c5e466882060a38ac0f3475811e98
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="846b0-104">De versie die voorjaar opstarten Starter gebruiken met Azure Cosmos DB DocumentDB-API</span><span class="sxs-lookup"><span data-stu-id="846b0-104">How to use the Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="846b0-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="846b0-105">Overview</span></span>

<span data-ttu-id="846b0-106">De  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="846b0-106">The **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="846b0-107">Een van de meer populaire projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="846b0-107">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="846b0-108">Om te helpen aan de slag met Spring opstarten ontwikkelaars, verschillende voorbeeld Spring opstarten pakketten zijn beschikbaar op <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="846b0-108">To help developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="846b0-109">Naast de kiezen uit de lijst met basic Spring opstarten projecten, de  **[Spring Initializr]**  kunnen softwareontwikkelaars aan de slag met het maken van aangepaste Spring Boot-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="846b0-109">In addition to choosing from the list of basic Spring Boot projects, the **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="846b0-110">Azure Cosmos-database is een globaal gedistribueerd database-service waarmee ontwikkelaars kunnen werken met gegevens met verschillende standaard API's, zoals DocumentDB, MongoDB, grafiek en tabel-API's.</span><span class="sxs-lookup"><span data-stu-id="846b0-110">Azure Cosmos DB is a globally-distributed database service that allows developers to work with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="846b0-111">Microsoft versie die voorjaar opstarten Starter kunnen ontwikkelaars eenvoudig worden geïntegreerd met Azure Cosmos DB met behulp van DocumentDB APIs Spring opstarten toepassingen.</span><span class="sxs-lookup"><span data-stu-id="846b0-111">Microsoft's Spring Boot Starter enables developers to use Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="846b0-112">Dit artikel wordt beschreven voor het maken van een Cosmos Azure DB de Azure-portal gebruikt, is met behulp van de **Spring Initializr** een aangepaste java-toepassing maken en vervolgens de Spring opstarten Starter-functionaliteit toe te voegen aan uw aangepaste toepassing voor het opslaan van gegevens in en gegevens ophalen van de Cosmos Azure DB met behulp van de DocumentDB-API.</span><span class="sxs-lookup"><span data-stu-id="846b0-112">This article demonstrates creating an Azure Cosmos DB using the Azure portal, then using the **Spring Initializr** to create a custom java application, and then add the Spring Boot Starter functionality to your custom application to store data in and retrieve data from your Azure Cosmos DB by using the DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="846b0-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="846b0-113">Prerequisites</span></span>

<span data-ttu-id="846b0-114">De volgende vereisten zijn vereist voor de stappen in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="846b0-114">The following prerequisites are required in order to follow the steps in this article:</span></span>

* <span data-ttu-id="846b0-115">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="846b0-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="846b0-116">Een [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="846b0-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="846b0-117">[Apache Maven](http://maven.apache.org/), versie 3.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="846b0-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-the-azure-portal"></a><span data-ttu-id="846b0-118">Een Azure-Cosmos-database maken met behulp van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="846b0-118">Create an Azure Cosmos DB by using the Azure portal</span></span>

1. <span data-ttu-id="846b0-119">Blader naar de Azure portal op <https://portal.azure.com/> en klik op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="846b0-119">Browse to the Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="846b0-121">Klik op **Databases**, en klik vervolgens op **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="846b0-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="846b0-123">Op de **Azure Cosmos DB** pagina, voer de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="846b0-123">On the **Azure Cosmos DB** page, enter the following information:</span></span>

   * <span data-ttu-id="846b0-124">Voer een unieke **ID**, gaat u als de URI voor uw database.</span><span class="sxs-lookup"><span data-stu-id="846b0-124">Enter a unique **ID**, which you will use as the URI for your database.</span></span> <span data-ttu-id="846b0-125">Bijvoorbeeld: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="846b0-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="846b0-126">Kies **SQL (Document DB)** voor de API.</span><span class="sxs-lookup"><span data-stu-id="846b0-126">Choose **SQL (Document DB)** for the API.</span></span>
   * <span data-ttu-id="846b0-127">Kies de **abonnement** u wilt gebruiken voor uw database.</span><span class="sxs-lookup"><span data-stu-id="846b0-127">Choose the **Subscription** you want to use for your database.</span></span>
   * <span data-ttu-id="846b0-128">Geef op of maak een nieuwe **resourcegroep** voor uw database, of kies een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="846b0-128">Specify whether to create a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="846b0-129">Geef de **locatie** voor uw database.</span><span class="sxs-lookup"><span data-stu-id="846b0-129">Specify the **Location** for your database.</span></span>
   
   <span data-ttu-id="846b0-130">Wanneer u deze opties hebt opgegeven, klikt u op **maken** om uw database te maken.</span><span class="sxs-lookup"><span data-stu-id="846b0-130">When you have specified these options, click **Create** to create your database.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="846b0-132">Wanneer uw database is gemaakt, wordt vermeld in uw Azure **Dashboard**, ook als onder de **alle Resources** en **Azure Cosmos DB** pagina's.</span><span class="sxs-lookup"><span data-stu-id="846b0-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under the **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="846b0-133">U kunt klikken op de database op een van deze locaties om de eigenschappenpagina voor uw cache te openen.</span><span class="sxs-lookup"><span data-stu-id="846b0-133">You can click on your database on any of those locations to open the properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="846b0-135">Wanneer de eigenschappenpagina voor uw database wordt weergegeven, klikt u op **toegangssleutels** en kopieer uw URI en toegangssleutels voor uw database; u kunt deze waarden worden gebruikt in uw toepassing Spring opstarten.</span><span class="sxs-lookup"><span data-stu-id="846b0-135">When the properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-the-spring-initializr"></a><span data-ttu-id="846b0-137">Een eenvoudige Spring Boot-toepassing maken met de versie die voorjaar Initializr</span><span class="sxs-lookup"><span data-stu-id="846b0-137">Create a simple Spring Boot application with the Spring Initializr</span></span>

1. <span data-ttu-id="846b0-138">Blader naar <https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="846b0-138">Browse to <https://start.spring.io/>.</span></span>

1. <span data-ttu-id="846b0-139">Opgeven dat u voor het genereren van een **Maven** project met **Java**, voer de **groep** en **artefact** namen voor uw toepassing en klik vervolgens op de knop **genereren Project**.</span><span class="sxs-lookup"><span data-stu-id="846b0-139">Specify that you want to generate a **Maven** project with **Java**, enter the **Group** and **Artifact** names for your application, and then click the button to **Generate Project**.</span></span>

   ![Basic Spring Initializr opties][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="846b0-141">De versie die voorjaar Initializr gebruikt de **groep** en **artefact** namen voor het maken van de naam van het pakket; bijvoorbeeld: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="846b0-141">The Spring Initializr uses the **Group** and **Artifact** names to create the package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="846b0-142">Wanneer u wordt gevraagd, download u het project naar een pad op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="846b0-142">When prompted, download the project to a path on your local computer.</span></span>

   ![Aangepaste Spring Boot-project downloaden][SI02]

1. <span data-ttu-id="846b0-144">Nadat u de bestanden op uw lokale system hebt uitgepakt, zal uw eenvoudige Spring Boot-toepassing gereed is voor het bewerken van zijn.</span><span class="sxs-lookup"><span data-stu-id="846b0-144">After you have extracted the files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Aangepaste Spring project opstartbestanden][SI03]

## <a name="configure-your-spring-boot-app-to-use-the-azure-spring-boot-starter"></a><span data-ttu-id="846b0-146">Configureer uw app Spring opstarten voor het gebruik van de Azure Spring opstarten Starter</span><span class="sxs-lookup"><span data-stu-id="846b0-146">Configure your Spring Boot app to use the Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="846b0-147">Zoek de *pom.xml* bestand in de map van uw app; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="846b0-147">Locate the *pom.xml* file in the directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="846b0-148">-of-</span><span class="sxs-lookup"><span data-stu-id="846b0-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Zoek het bestand pom.xml][PM01]

1. <span data-ttu-id="846b0-150">Open de *pom.xml* bestand in een teksteditor en de volgende regels toevoegen aan lijst met `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="846b0-150">Open the *pom.xml* file in a text editor, and add the following lines to list of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Het bestand pom.xml bewerken][PM02]

1. <span data-ttu-id="846b0-152">Sla op en sluit de *pom.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-152">Save and close the *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-to-use-your-azure-cosmos-db"></a><span data-ttu-id="846b0-153">Configureer uw app Spring opstarten voor het gebruik van uw Azure-Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="846b0-153">Configure your Spring Boot app to use your Azure Cosmos DB</span></span>

1. <span data-ttu-id="846b0-154">Zoek de *application.properties* bestand de *resources* map van uw app; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="846b0-154">Locate the *application.properties* file in the *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="846b0-155">-of-</span><span class="sxs-lookup"><span data-stu-id="846b0-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Zoek het bestand application.properties][RE01]

1. <span data-ttu-id="846b0-157">Open de *application.properties* bestand in een teksteditor en de volgende regels toevoegen aan het bestand en de voorbeeldwaarden vervangen door de juiste eigenschappen voor uw database:</span><span class="sxs-lookup"><span data-stu-id="846b0-157">Open the *application.properties* file in a text editor, and add the following lines to the file, and replace the sample values with the appropriate properties for your database:</span></span>

   ```yaml
   # Specify the DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify the access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify the name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Bewerken van het bestand application.properties][RE02]

1. <span data-ttu-id="846b0-159">Sla op en sluit de *application.properties* bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-159">Save and close the *application.properties* file.</span></span>

## <a name="add-sample-code-to-implement-basic-database-functionality"></a><span data-ttu-id="846b0-160">Voorbeeldcode voor het implementeren van eenvoudige databasefunctionaliteit toevoegen</span><span class="sxs-lookup"><span data-stu-id="846b0-160">Add sample code to implement basic database functionality</span></span>

<span data-ttu-id="846b0-161">In deze sectie maakt u twee Java-klassen voor het opslaan van gebruikersgegevens en wijzig vervolgens de hoofdtoepassingsklasse voor het maken van een exemplaar van de gebruikersklasse en sla deze op uw database.</span><span class="sxs-lookup"><span data-stu-id="846b0-161">In this section you create two Java classes for storing user data, and then you modify your main application class to create an instance of the user class and save it to your database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="846b0-162">Een eenvoudige klasse voor het opslaan van gebruikersgegevens definiëren</span><span class="sxs-lookup"><span data-stu-id="846b0-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="846b0-163">Maak een nieuw bestand met de naam *User.java* in dezelfde map als de hoofdtoepassing Java-bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-163">Create a new file named *User.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="846b0-164">Open de *User.java* bestand in een teksteditor en voeg de volgende regels in het bestand voor het definiëren van een algemene gebruikersklasse die worden opgeslagen en ophalen van waarden in de database:</span><span class="sxs-lookup"><span data-stu-id="846b0-164">Open the *User.java* file in a text editor, and add the following lines to the file to define a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="846b0-165">Sla op en sluit de *User.java* bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-165">Save and close the *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="846b0-166">Definieer een interface-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="846b0-166">Define a data repository interface</span></span>

1. <span data-ttu-id="846b0-167">Maak een nieuw bestand met de naam *UserRepository.java* in dezelfde map als de hoofdtoepassing Java-bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-167">Create a new file named *UserRepository.java* in the same directory as your main application Java file.</span></span>

1. <span data-ttu-id="846b0-168">Open de *UserRepository.java* bestand in een teksteditor en voeg de volgende regels in het bestand voor het definiëren van een gebruikersinterface van de opslagplaats die uitgebreider is dan de standaardinterface voor DocumentDB-opslagplaats:</span><span class="sxs-lookup"><span data-stu-id="846b0-168">Open the *UserRepository.java* file in a text editor, and add the following lines to the file to define a user repository interface that extends the default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="846b0-169">Sla op en sluit de *UserRepository.java* bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-169">Save and close the *UserRepository.java* file.</span></span>

### <a name="modify-the-main-application-class"></a><span data-ttu-id="846b0-170">Wijzigen van de hoofdtoepassing-klasse</span><span class="sxs-lookup"><span data-stu-id="846b0-170">Modify the main application class</span></span>

1. <span data-ttu-id="846b0-171">Zoek het hoofdvenster van de toepassing Java-bestand in de pakketmap van uw app; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="846b0-171">Locate the main application Java file in the package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="846b0-172">-of-</span><span class="sxs-lookup"><span data-stu-id="846b0-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Zoek de Java-bestand van de toepassing][JV01]

1. <span data-ttu-id="846b0-174">Open het hoofdvenster van de toepassing Java-bestand in een teksteditor en voeg de volgende regels in het bestand:</span><span class="sxs-lookup"><span data-stu-id="846b0-174">Open the main application Java file in a text editor, and add the following lines to the file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="846b0-175">Opslaan en sluiten van de hoofdtoepassing Java-bestand.</span><span class="sxs-lookup"><span data-stu-id="846b0-175">Save and close the main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="846b0-176">Bouwen en testen van uw app</span><span class="sxs-lookup"><span data-stu-id="846b0-176">Build and test your app</span></span>

1. <span data-ttu-id="846b0-177">Open een opdrachtprompt en wijzig de map naar de map waar uw *pom.xml* bestand bevindt zich; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="846b0-177">Open a command prompt and change directory to the folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="846b0-178">-of-</span><span class="sxs-lookup"><span data-stu-id="846b0-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="846b0-179">Uw toepassing Spring opstarten met Maven bouwen en uitvoeren. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="846b0-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="846b0-180">Uw toepassing meerdere runtime-berichten worden weergegeven en u ziet het bericht `User: testFirstName testLastName` weergegeven om aan te geven waarden met succes is opgeslagen en opgehaald uit de database.</span><span class="sxs-lookup"><span data-stu-id="846b0-180">Your application will display several runtime messages, and you should see the message `User: testFirstName testLastName` displayed to indicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Geslaagde uitvoer van de toepassing][JV02]

1. <span data-ttu-id="846b0-182">Optioneel: U kunt de Azure-portal de inhoud van uw Azure-Cosmos-DB uit de eigenschappenpagina voor uw database weergeven door te klikken op **documentverkenner**, en vervolgens te selecteren en item uit de vervolgkeuzelijst om de inhoud weer te geven.</span><span class="sxs-lookup"><span data-stu-id="846b0-182">OPTIONAL: You can use the Azure portal to view the contents of your Azure Cosmos DB from the properties page for your database by clicking  **Document Explorer**, and then selecting and item from the displayed list to view the contents.</span></span>

   ![Met behulp van de documentverkenner om uw gegevens weer te geven][JV03]

## <a name="next-steps"></a><span data-ttu-id="846b0-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="846b0-184">Next steps</span></span>

<span data-ttu-id="846b0-185">Zie de volgende artikelen voor meer informatie over het gebruik van Azure DB die Cosmos en Java:</span><span class="sxs-lookup"><span data-stu-id="846b0-185">For more information about using Azure Cosmos DB and Java, see the following articles:</span></span>

* <span data-ttu-id="846b0-186">[Documentatie Azure Cosmos DB].</span><span class="sxs-lookup"><span data-stu-id="846b0-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="846b0-187">[Azure Cosmos DB: Een DocumentDB-API-app met Java en de Azure portal maken][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="846b0-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and the Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="846b0-188">Zie de volgende artikelen voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure:</span><span class="sxs-lookup"><span data-stu-id="846b0-188">For more information about using Spring Boot applications on Azure, see the following articles:</span></span>

* [<span data-ttu-id="846b0-189">Spring Boot DocumenDB Starter voor Azure</span><span class="sxs-lookup"><span data-stu-id="846b0-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="846b0-190">Een toepassing Spring opstart in de Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="846b0-190">Deploy a Spring Boot Application to the Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="846b0-191">Spring opstarten toepassing uitvoert op een Cluster Kubernetes in de Azure Containerservice</span><span class="sxs-lookup"><span data-stu-id="846b0-191">Running a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="846b0-192">Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="846b0-192">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

<span data-ttu-id="846b0-193">[Documentatie Azure Cosmos DB]: /azure/cosmos-db/</span><span class="sxs-lookup"><span data-stu-id="846b0-193">[Azure Cosmos DB Documentation]: /azure/cosmos-db/</span></span>
<span data-ttu-id="846b0-194">[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="846b0-194">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
<span data-ttu-id="846b0-195">[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="846b0-195">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="846b0-196">[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="846b0-196">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="846b0-197">[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="846b0-197">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="846b0-198">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="846b0-198">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="846b0-199">[Spring Initializr]: https://start.spring.io/</span><span class="sxs-lookup"><span data-stu-id="846b0-199">[Spring Initializr]: https://start.spring.io/</span></span>
<span data-ttu-id="846b0-200">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="846b0-200">[Spring Framework]: https://spring.io/</span></span>

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
