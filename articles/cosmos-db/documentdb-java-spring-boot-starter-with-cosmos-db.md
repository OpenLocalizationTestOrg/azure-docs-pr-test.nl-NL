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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Hoe toouse Hallo Spring opstarten Starter met DocumentDB-API van Azure Cosmos DB

## <a name="overview"></a>Overzicht

Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen. toohelp ontwikkelaars aan de slag met Spring opstarten, verschillende voorbeeld Spring opstarten pakketten zijn beschikbaar op <https://github.com/spring-guides/>. Bovendien toochoosing uit de lijst Hallo van basic Spring opstartinstallatiekopie projecten, hello  **[Spring Initializr]**  kunnen softwareontwikkelaars aan de slag met het maken van aangepaste Spring Boot-toepassingen.

Azure Cosmos-database is een globaal gedistribueerd database-service waarmee ontwikkelaars toowork met gegevens met verschillende standaard API's, zoals DocumentDB, MongoDB, grafiek en tabel-API's. Microsoft versie die voorjaar opstarten Starter kunnen ontwikkelaars toouse Spring opstarten toepassingen die eenvoudig kunt met Azure Cosmos DB integreren met behulp van DocumentDB APIs.

Dit artikel wordt beschreven voor het maken van een Cosmos Azure DB hello Azure-portal gebruikt, is met behulp van Hallo **Spring Initializr** toocreate een aangepaste java-toepassing en voeg vervolgens Hallo Spring opstarten Starter functionaliteit tooyour aangepast Hallo DocumentDB API toepassing toostore gegevens in en opgehaald uit de database van uw Azure Cosmos door gebruik te maken.

## <a name="prerequisites"></a>Vereisten

Hallo volgende vereiste onderdelen zijn vereist in de volgorde toofollow Hallo stappen in dit artikel:

* Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].

* Een [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 of hoger.

* [Apache Maven](http://maven.apache.org/), versie 3.0 of hoger.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Een Azure-Cosmos-database maken met behulp van hello Azure-portal

1. Blader toohello Azure portal op <https://portal.azure.com/> en klik op **+ nieuw**.

   ![Azure Portal][AZ01]

1. Klik op **Databases**, en klik vervolgens op **Azure Cosmos DB**.

   ![Azure Portal][AZ02]

1. Op Hallo **Azure Cosmos DB** pagina, voert u Hallo volgende informatie:

   * Voer een unieke **ID**, gaat u als Hallo URI voor uw database. Bijvoorbeeld: *wingtiptoysdata.documents.azure.com*.
   * Kies **SQL (Document DB)** voor Hallo API.
   * Kies Hallo **abonnement** gewenste toouse voor uw database.
   * Opgeven of toocreate een nieuwe **resourcegroep** voor uw database, of kies een bestaande resourcegroep.
   * Geef Hallo **locatie** voor uw database.
   
   Wanneer u deze opties hebt opgegeven, klikt u op **maken** toocreate uw database.

   ![Azure Portal][AZ03]

1. Wanneer uw database is gemaakt, wordt vermeld in uw Azure **Dashboard**, evenals in Hallo **alle Resources** en **Azure Cosmos DB** pagina's. U kunt klikken op de database op een van deze locaties tooopen Hallo-pagina met eigenschappen voor uw cache.

   ![Azure Portal][AZ04]

1. Wanneer de eigenschappenpagina Hallo voor uw database wordt weergegeven, klikt u op **toegangssleutels** en kopieer uw URI en toegangssleutels voor uw database; u kunt deze waarden worden gebruikt in uw toepassing Spring opstarten.

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Een eenvoudige Spring Boot-toepassing Hello Spring Initializr maken

1. Te bladeren<https://start.spring.io/>.

1. U wilt opgeven dat toogenerate een **Maven** project met **Java**, Voer Hallo **groep** en **artefact** namen voor uw toepassing en Klik vervolgens op Hallo te**genereren Project**.

   ![Basic Spring Initializr opties][SI01]

   > [!NOTE]
   >
   > Hallo Spring Initializr gebruikt Hallo **groep** en **artefact** namen toocreate Hallo pakketnaam; bijvoorbeeld: *com.example.wintiptoys*.
   >

1. Wanneer u wordt gevraagd, downloadpad Hallo project tooa op uw lokale computer.

   ![Aangepaste Spring Boot-project downloaden][SI02]

1. Nadat u Hallo-bestanden op uw lokale systeem hebt uitgepakt, worden uw eenvoudige Spring Boot-toepassing gereed is voor het bewerken.

   ![Aangepaste Spring project opstartbestanden][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Uw Spring opstarten app toouse hello Azure Spring opstarten Starter configureren

1. Zoek Hallo *pom.xml* bestand in map Hallo van uw app; bijvoorbeeld:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   -of-

   `/users/example/home/wingtiptoys/pom.xml`

   ![Ga naar Hallo pom.xml-bestand][PM01]

1. Open Hallo *pom.xml* bestand in een teksteditor en voeg Hallo toolist regels van de volgende `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Hallo pom.xml-bestand bewerken][PM02]

1. Opslaan en sluiten Hallo *pom.xml* bestand.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Configureer uw app Spring Boot toouse uw Cosmos Azure DB

1. Zoek Hallo *application.properties* bestand in Hallo *resources* map van uw app; bijvoorbeeld:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   -of-

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Hallo application.properties bestand gevonden][RE01]

1. Open Hallo *application.properties* bestand in een teksteditor en Hallo voorbeeldwaarden vervangen door Hallo toepasselijke eigenschappen voor uw database Hallo volgende toohello regels toevoegen:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Hallo application.properties bestand bewerken][RE02]

1. Opslaan en sluiten Hallo *application.properties* bestand.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Voorbeeld code tooimplement basic databasefunctionaliteit toevoegen

In deze sectie maakt u twee Java-klassen voor het opslaan van gebruikersgegevens, en vervolgens uw hoofdtoepassing klasse toocreate een exemplaar van de gebruikersklasse Hallo wijzigen en deze tooyour database opslaan.

### <a name="define-a-basic-class-for-storing-user-data"></a>Een eenvoudige klasse voor het opslaan van gebruikersgegevens definiëren

1. Maak een nieuw bestand met de naam *User.java* in Hallo dezelfde map als de hoofdtoepassing Java-bestand.

1. Open Hallo *User.java* bestand in een teksteditor en voeg de volgende Hallo regels toohello bestand toodefine een algemene gebruikersklasse die worden opgeslagen en ophalen van waarden in de database:

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

1. Opslaan en sluiten Hallo *User.java* bestand.

### <a name="define-a-data-repository-interface"></a>Definieer een interface-opslagplaats

1. Maak een nieuw bestand met de naam *UserRepository.java* in Hallo dezelfde map als de hoofdtoepassing Java-bestand.

1. Open Hallo *UserRepository.java* bestand in een teksteditor en voeg de volgende Hallo regels toohello bestand toodefine opslagplaats met een gebruikersinterface die uitgebreider is DocumentDB Hallo-opslagplaats standaardinterface:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Opslaan en sluiten Hallo *UserRepository.java* bestand.

### <a name="modify-hello-main-application-class"></a>Hallo hoofdtoepassingsklasse wijzigen

1. Hallo Java hoofdtoepassingsbestand niet vinden in de pakketmap Hallo van uw app; bijvoorbeeld:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   -of-

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Hallo-toepassingsbestand Java vinden][JV01]

1. Hallo Java hoofdtoepassingsbestand openen in een teksteditor en Hallo volgende toohello regels toevoegen:

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

1. Opslaan en sluiten Hallo Java hoofdtoepassingsbestand.

## <a name="build-and-test-your-app"></a>Bouwen en testen van uw app

1. Open een opdrachtprompt en wijzig map toohello waar uw *pom.xml* bestand bevindt zich; bijvoorbeeld:

   `cd C:\SpringBoot\wingtiptoys`

   -of-

   `cd /users/example/home/wingtiptoys`

1. Uw toepassing Spring opstarten met Maven bouwen en uitvoeren. bijvoorbeeld:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. Uw toepassing meerdere runtime-berichten worden weergegeven en ziet u het Hallo-bericht `User: testFirstName testLastName` tooindicate waarden met succes is opgeslagen en opgehaald uit de database weergegeven.

   ![Geslaagde uitvoer van de toepassing hello][JV02]

1. Optioneel: U kunt hello Azure portal tooview Hallo inhoud van uw Azure-Cosmos-DB van eigenschappenpagina Hallo voor uw database door te klikken op **documentverkenner**, en vervolgens te selecteren en item uit Hallo weergegeven lijst tooview Hallo de inhoud.

   ![Met behulp van Hallo documentverkenner tooview uw gegevens][JV03]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van Azure DB die Cosmos en Java Hallo artikelen te volgen:

* [Documentatie Azure Cosmos DB].

* [Azure Cosmos DB: Een DocumentDB-API-App met behulp van Java en hello Azure-portal][Build a DocumentDB API app with Java]

Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:

* [Spring Boot DocumenDB Starter voor Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Een versie die voorjaar opstarten toepassing uitvoert in een Kubernetes Cluster in hello Azure Container Service](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

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
