---
title: aaaHow toouse Hallo Spring opstarten Starter met een Azure-API voor DocumentDB Cosmos DB
description: Meer informatie over hoe tooconfigure een toepassing gemaakt met de Hallo Spring opstarten initialisatiefunctie Hello Azure Cosmos DB DocumentDB API.
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
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="8ab98-104">Hoe toouse Hallo Spring opstarten Starter met DocumentDB-API van Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="8ab98-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="8ab98-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="8ab98-105">Overview</span></span>

<span data-ttu-id="8ab98-106">Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="8ab98-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="8ab98-107">Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8ab98-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="8ab98-108">toohelp ontwikkelaars aan de slag met Spring opstarten, verschillende voorbeeld Spring opstarten pakketten zijn beschikbaar op <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="8ab98-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="8ab98-109">Bovendien toochoosing uit de lijst Hallo van basic Spring opstartinstallatiekopie projecten, hello  **[Spring Initializr]**  kunnen softwareontwikkelaars aan de slag met het maken van aangepaste Spring Boot-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="8ab98-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="8ab98-110">Azure Cosmos-database is een globaal gedistribueerd database-service waarmee ontwikkelaars toowork met gegevens met verschillende standaard API's, zoals DocumentDB, MongoDB, grafiek en tabel-API's.</span><span class="sxs-lookup"><span data-stu-id="8ab98-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="8ab98-111">Microsoft versie die voorjaar opstarten Starter kunnen ontwikkelaars toouse Spring opstarten toepassingen die eenvoudig kunt met Azure Cosmos DB integreren met behulp van DocumentDB APIs.</span><span class="sxs-lookup"><span data-stu-id="8ab98-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="8ab98-112">Dit artikel wordt beschreven voor het maken van een Cosmos Azure DB hello Azure-portal gebruikt, is met behulp van Hallo **Spring Initializr** toocreate een aangepaste java-toepassing en voeg vervolgens Hallo Spring opstarten Starter functionaliteit tooyour aangepast Hallo DocumentDB API toepassing toostore gegevens in en opgehaald uit de database van uw Azure Cosmos door gebruik te maken.</span><span class="sxs-lookup"><span data-stu-id="8ab98-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ab98-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8ab98-113">Prerequisites</span></span>

<span data-ttu-id="8ab98-114">Hallo volgende vereiste onderdelen zijn vereist in de volgorde toofollow Hallo stappen in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="8ab98-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="8ab98-115">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="8ab98-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="8ab98-116">Een [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8ab98-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="8ab98-117">[Apache Maven](http://maven.apache.org/), versie 3.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8ab98-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="8ab98-118">Een Azure-Cosmos-database maken met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8ab98-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="8ab98-119">Blader toohello Azure portal op <https://portal.azure.com/> en klik op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="8ab98-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="8ab98-121">Klik op **Databases**, en klik vervolgens op **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="8ab98-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="8ab98-123">Op Hallo **Azure Cosmos DB** pagina, voert u Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="8ab98-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="8ab98-124">Voer een unieke **ID**, gaat u als Hallo URI voor uw database.</span><span class="sxs-lookup"><span data-stu-id="8ab98-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="8ab98-125">Bijvoorbeeld: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="8ab98-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="8ab98-126">Kies **SQL (Document DB)** voor Hallo API.</span><span class="sxs-lookup"><span data-stu-id="8ab98-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="8ab98-127">Kies Hallo **abonnement** gewenste toouse voor uw database.</span><span class="sxs-lookup"><span data-stu-id="8ab98-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="8ab98-128">Opgeven of toocreate een nieuwe **resourcegroep** voor uw database, of kies een bestaande resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8ab98-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="8ab98-129">Geef Hallo **locatie** voor uw database.</span><span class="sxs-lookup"><span data-stu-id="8ab98-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="8ab98-130">Wanneer u deze opties hebt opgegeven, klikt u op **maken** toocreate uw database.</span><span class="sxs-lookup"><span data-stu-id="8ab98-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="8ab98-132">Wanneer uw database is gemaakt, wordt vermeld in uw Azure **Dashboard**, evenals in Hallo **alle Resources** en **Azure Cosmos DB** pagina's.</span><span class="sxs-lookup"><span data-stu-id="8ab98-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="8ab98-133">U kunt klikken op de database op een van deze locaties tooopen Hallo-pagina met eigenschappen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="8ab98-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="8ab98-135">Wanneer de eigenschappenpagina Hallo voor uw database wordt weergegeven, klikt u op **toegangssleutels** en kopieer uw URI en toegangssleutels voor uw database; u kunt deze waarden worden gebruikt in uw toepassing Spring opstarten.</span><span class="sxs-lookup"><span data-stu-id="8ab98-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="8ab98-137">Een eenvoudige Spring Boot-toepassing Hello Spring Initializr maken</span><span class="sxs-lookup"><span data-stu-id="8ab98-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="8ab98-138">Te bladeren<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="8ab98-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="8ab98-139">U wilt opgeven dat toogenerate een **Maven** project met **Java**, Voer Hallo **groep** en **artefact** namen voor uw toepassing en Klik vervolgens op Hallo te**genereren Project**.</span><span class="sxs-lookup"><span data-stu-id="8ab98-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Basic Spring Initializr opties][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="8ab98-141">Hallo Spring Initializr gebruikt Hallo **groep** en **artefact** namen toocreate Hallo pakketnaam; bijvoorbeeld: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="8ab98-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="8ab98-142">Wanneer u wordt gevraagd, downloadpad Hallo project tooa op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="8ab98-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Aangepaste Spring Boot-project downloaden][SI02]

1. <span data-ttu-id="8ab98-144">Nadat u Hallo-bestanden op uw lokale systeem hebt uitgepakt, worden uw eenvoudige Spring Boot-toepassing gereed is voor het bewerken.</span><span class="sxs-lookup"><span data-stu-id="8ab98-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Aangepaste Spring project opstartbestanden][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="8ab98-146">Uw Spring opstarten app toouse hello Azure Spring opstarten Starter configureren</span><span class="sxs-lookup"><span data-stu-id="8ab98-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="8ab98-147">Zoek Hallo *pom.xml* bestand in map Hallo van uw app; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8ab98-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="8ab98-148">-of-</span><span class="sxs-lookup"><span data-stu-id="8ab98-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Ga naar Hallo pom.xml-bestand][PM01]

1. <span data-ttu-id="8ab98-150">Open Hallo *pom.xml* bestand in een teksteditor en voeg Hallo toolist regels van de volgende `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="8ab98-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Hallo pom.xml-bestand bewerken][PM02]

1. <span data-ttu-id="8ab98-152">Opslaan en sluiten Hallo *pom.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="8ab98-153">Configureer uw app Spring Boot toouse uw Cosmos Azure DB</span><span class="sxs-lookup"><span data-stu-id="8ab98-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="8ab98-154">Zoek Hallo *application.properties* bestand in Hallo *resources* map van uw app; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8ab98-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="8ab98-155">-of-</span><span class="sxs-lookup"><span data-stu-id="8ab98-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Hallo application.properties bestand gevonden][RE01]

1. <span data-ttu-id="8ab98-157">Open Hallo *application.properties* bestand in een teksteditor en Hallo voorbeeldwaarden vervangen door Hallo toepasselijke eigenschappen voor uw database Hallo volgende toohello regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8ab98-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Hallo application.properties bestand bewerken][RE02]

1. <span data-ttu-id="8ab98-159">Opslaan en sluiten Hallo *application.properties* bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="8ab98-160">Voorbeeld code tooimplement basic databasefunctionaliteit toevoegen</span><span class="sxs-lookup"><span data-stu-id="8ab98-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="8ab98-161">In deze sectie maakt u twee Java-klassen voor het opslaan van gebruikersgegevens, en vervolgens uw hoofdtoepassing klasse toocreate een exemplaar van de gebruikersklasse Hallo wijzigen en deze tooyour database opslaan.</span><span class="sxs-lookup"><span data-stu-id="8ab98-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="8ab98-162">Een eenvoudige klasse voor het opslaan van gebruikersgegevens definiëren</span><span class="sxs-lookup"><span data-stu-id="8ab98-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="8ab98-163">Maak een nieuw bestand met de naam *User.java* in Hallo dezelfde map als de hoofdtoepassing Java-bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="8ab98-164">Open Hallo *User.java* bestand in een teksteditor en voeg de volgende Hallo regels toohello bestand toodefine een algemene gebruikersklasse die worden opgeslagen en ophalen van waarden in de database:</span><span class="sxs-lookup"><span data-stu-id="8ab98-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

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

1. <span data-ttu-id="8ab98-165">Opslaan en sluiten Hallo *User.java* bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="8ab98-166">Definieer een interface-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="8ab98-166">Define a data repository interface</span></span>

1. <span data-ttu-id="8ab98-167">Maak een nieuw bestand met de naam *UserRepository.java* in Hallo dezelfde map als de hoofdtoepassing Java-bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="8ab98-168">Open Hallo *UserRepository.java* bestand in een teksteditor en voeg de volgende Hallo regels toohello bestand toodefine opslagplaats met een gebruikersinterface die uitgebreider is DocumentDB Hallo-opslagplaats standaardinterface:</span><span class="sxs-lookup"><span data-stu-id="8ab98-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="8ab98-169">Opslaan en sluiten Hallo *UserRepository.java* bestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="8ab98-170">Hallo hoofdtoepassingsklasse wijzigen</span><span class="sxs-lookup"><span data-stu-id="8ab98-170">Modify hello main application class</span></span>

1. <span data-ttu-id="8ab98-171">Hallo Java hoofdtoepassingsbestand niet vinden in de pakketmap Hallo van uw app; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8ab98-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="8ab98-172">-of-</span><span class="sxs-lookup"><span data-stu-id="8ab98-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Hallo-toepassingsbestand Java vinden][JV01]

1. <span data-ttu-id="8ab98-174">Hallo Java hoofdtoepassingsbestand openen in een teksteditor en Hallo volgende toohello regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="8ab98-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

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

1. <span data-ttu-id="8ab98-175">Opslaan en sluiten Hallo Java hoofdtoepassingsbestand.</span><span class="sxs-lookup"><span data-stu-id="8ab98-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="8ab98-176">Bouwen en testen van uw app</span><span class="sxs-lookup"><span data-stu-id="8ab98-176">Build and test your app</span></span>

1. <span data-ttu-id="8ab98-177">Open een opdrachtprompt en wijzig map toohello waar uw *pom.xml* bestand bevindt zich; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8ab98-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="8ab98-178">-of-</span><span class="sxs-lookup"><span data-stu-id="8ab98-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="8ab98-179">Uw toepassing Spring opstarten met Maven bouwen en uitvoeren. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8ab98-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="8ab98-180">Uw toepassing meerdere runtime-berichten worden weergegeven en ziet u het Hallo-bericht `User: testFirstName testLastName` tooindicate waarden met succes is opgeslagen en opgehaald uit de database weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8ab98-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Geslaagde uitvoer van de toepassing hello][JV02]

1. <span data-ttu-id="8ab98-182">Optioneel: U kunt hello Azure portal tooview Hallo inhoud van uw Azure-Cosmos-DB van eigenschappenpagina Hallo voor uw database door te klikken op **documentverkenner**, en vervolgens te selecteren en item uit Hallo weergegeven lijst tooview Hallo de inhoud.</span><span class="sxs-lookup"><span data-stu-id="8ab98-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![Met behulp van Hallo documentverkenner tooview uw gegevens][JV03]

## <a name="next-steps"></a><span data-ttu-id="8ab98-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8ab98-184">Next steps</span></span>

<span data-ttu-id="8ab98-185">Zie voor meer informatie over het gebruik van Azure DB die Cosmos en Java Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ab98-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="8ab98-186">[Documentatie Azure Cosmos DB].</span><span class="sxs-lookup"><span data-stu-id="8ab98-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="8ab98-187">[Azure Cosmos DB: Een DocumentDB-API-App met behulp van Java en hello Azure-portal][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="8ab98-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="8ab98-188">Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8ab98-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="8ab98-189">Spring Boot DocumenDB Starter voor Azure</span><span class="sxs-lookup"><span data-stu-id="8ab98-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="8ab98-190">Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="8ab98-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="8ab98-191">Een versie die voorjaar opstarten toepassing uitvoert in een Kubernetes Cluster in hello Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="8ab98-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="8ab98-192">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="8ab98-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Documentatie Azure Cosmos DB]: /azure/cosmos-db/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

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
