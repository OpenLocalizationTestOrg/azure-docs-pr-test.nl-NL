---
title: aaaHow tooconfigure een versie die voorjaar opstarten initialisatiefunctie app toouse Redis-Cache
description: Meer informatie over hoe tooconfigure een versie die voorjaar opstarten toepassing gemaakt met Hallo Spring Initializr toouse Azure Redis-Cache.
services: redis-cache
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: Spring, Spring opstarten Starter, Redis-Cache
ms.assetid: 
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: java
ms.topic: article
ms.date: 7/21/2017
ms.author: robmcm;zhijzhao;yidon
ms.openlocfilehash: ad532c88d2d67b97079eeb0e0e392add29ac365b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a>Hoe tooconfigure een versie die voorjaar opstarten initialisatiefunctie app toouse Redis-Cache

## <a name="overview"></a>Overzicht

Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een van meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen. toohelp ontwikkelaars aan de slag met Spring opstarten, verschillende voorbeeld Spring opstarten pakketten zijn beschikbaar op <https://github.com/spring-guides/>. Bovendien toochoosing uit de lijst Hallo van basic Spring opstartinstallatiekopie projecten, hello  **[Spring Initializr]**  kunnen softwareontwikkelaars aan de slag met het maken van aangepaste Spring Boot-toepassingen.

Dit artikel begeleidt u bij het maken van een Redis-cache met behulp van Azure-portal met behulp van Hallo Hallo **Spring Initializr** toocreate een aangepaste toepassing, en maak vervolgens een Java-webtoepassing die zijn opgeslagen en opgehaald van de gegevens met uw Redis-cache.

## <a name="prerequisites"></a>Vereisten

Hallo volgende vereiste onderdelen zijn vereist in de volgorde toofollow Hallo stappen in dit artikel:

* Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].

* Een [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 of hoger.

* [Apache Maven](http://maven.apache.org/), versie 3.0 of hoger.

## <a name="create-a-redis-cache-on-azure"></a>Een Redis-cache maken op Azure

1. Blader toohello Azure portal op <https://portal.azure.com/> en klikt u op Hallo-item voor **+ nieuw**.

   ![Azure Portal][AZ01]

1. Klik op **Database**, en klik vervolgens op **Redis-Cache**.

   ![Azure Portal][AZ02]

1. Op Hallo **nieuwe Redis-Cache** pagina, voert u Hallo **DNS-naam** voor uw cache geeft uw **abonnement**, **resourcegroep**,  **Locatie**, en **prijscategorie**. Wanneer u deze opties hebt opgegeven, klikt u op **maken** toocreate uw cache.

   ![Azure Portal][AZ03]

1. Nadat uw cache is voltooid, ziet u het weergegeven in uw Azure **Dashboard**, evenals in Hallo **alle Resources**, en **Redis-Caches** pagina's. U kunt klikken op uw cache op een van deze locaties tooopen Hallo-pagina met eigenschappen voor uw cache.

   ![Azure Portal][AZ04]

1. Wanneer het Hallo-pagina met Hallo-lijst van eigenschappen voor uw cache wordt weergegeven, klikt u op **toegangssleutels** en kopieer uw toegangssleutels voor uw cache.

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a>Een aangepaste toepassing maken met behulp Hallo Spring Initializr

1. Te bladeren<https://start.spring.io/>.

1. U wilt opgeven dat toogenerate een **Maven** project met **Java**, Voer Hallo **groep** en **Aritifact** namen voor uw toepassing en klik vervolgens op Hallo-koppeling te**Switch toohello volledige versie** Hallo Spring Initializr.

   ![Basic Spring Initializr opties][SI01]

   > [!NOTE]
   >
   > Hallo Spring Initializr gebruikt Hallo **groep** en **Aritifact** namen toocreate Hallo pakketnaam; bijvoorbeeld: *com.contoso.myazuredemo*.
   >

1. Schuif omlaag toohello **Web** sectie en het selectievakje in voor Hallo **Web**, schuif naar beneden toohello **NoSQL** sectie en het selectievakje in voor Hallo **Redis**, schuif vervolgens toohello onder aan Hallo pagina en klik op Hallo te**genereren Project**.

   ![Opties voor volledige Spring Initializr][SI02]

1. Wanneer u wordt gevraagd, downloadpad Hallo project tooa op uw lokale computer.

   ![Aangepaste Spring Boot-project downloaden][SI03]

1. Nadat u hebt uitgepakt Hallo-bestanden op uw lokale systeem, zal uw aangepaste Spring Boot-toepassing gereed is voor het bewerken van zijn.

   ![Aangepaste Spring project opstartbestanden][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a>Uw aangepaste Spring Boot toouse uw Redis-Cache configureren

1. Zoek Hallo *application.properties* bestand in Hallo *resources* map van uw app of Hallo-bestand maken als deze niet al bestaat.

   ![Hallo application.properties bestand gevonden][RE01]

1. Open Hallo *application.properties* bestand in een teksteditor en Hallo voorbeeldwaarden vervangen door Hallo toepasselijke eigenschappen uit uw cache Hallo volgende toohello regels toevoegen:

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Hallo application.properties bestand bewerken][RE02]

1. Opslaan en sluiten Hallo *application.properties* bestand.

1. Maak een map met de naam *controller* onder Hallo bronmap voor het pakket; bijvoorbeeld:

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   -of-

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. Maak een nieuw bestand met de naam *HelloController.java* in Hallo *controller* map. Hallo-bestand openen in een teksteditor en voeg toe Hallo code tooit te volgen:

   ```java
   package com.contoso.myazuredemo;

   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   import org.springframework.beans.factory.annotation.Value;
   import redis.clients.jedis.Jedis;
   import redis.clients.jedis.JedisShardInfo;

   @RestController
   public class HelloController {
   
      // Retrieve hello DNS name for your cache.
      @Value("${spring.redis.host}")
      private String redisHost;

      // Retrieve hello port for your cache.
      @Value("${spring.redis.port}")
      private int redisPort;

      // Retrieve hello access key for your cache.
      @Value("${spring.redis.password}")
      private String redisPassword;

      @RequestMapping("/")
      // Define hello Hello World controller.
      public String hello() {
      
         // Create a JedisShardInfo object tooconnect tooyour Redis cache.
         JedisShardInfo jedisShardInfo = new JedisShardInfo(redisHost, redisPort, true);
         // Specify your access key.
         jedisShardInfo.setPassword(redisPassword);
         // Create a Jedis object toostore/retrieve information from your cache.
         Jedis jedis = new Jedis(jedisShardInfo);

         // Add a Hello World string tooyour cache.
         jedis.set("greeting", "Hello World!");

         // Return hello string from your cache.
         return jedis.get("greeting");
      }
   }
   ```
   
   Hier moet u tooreplace `com.contoso.myazuredemo` met Hallo pakketnaam voor uw project.

1. Opslaan en sluiten Hallo *HelloController.java* bestand.

1. Uw toepassing Spring opstarten met Maven bouwen en uitvoeren. bijvoorbeeld:

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. Hallo web-app testen door te bladeren toohttp://localhost:8080 met een webbrowser, of gebruik de syntaxis Hallo zoals Hallo na voorbeeld hebt u curl beschikbaar:

   ```shell
   curl http://localhost:8080
   ```

   U ziet Hallo "Hello World!" bericht ontvangen van uw voorbeeld-domeincontroller die wordt weergegeven, die dynamisch worden opgehaald uit de Redis-cache.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:

* [Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Een versie die voorjaar opstarten toepassing uitvoert in een Kubernetes Cluster in hello Azure Container Service](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

Zie voor meer informatie over het ophalen van de slag met Redis-Cache met behulp van Java in Azure, [hoe toouse Azure Redis-Cache met behulp van Java][Redis Cache with Java].

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/
[Redis Cache with Java]: cache-java-get-started.md

<!-- IMG List -->

[AZ01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ01.png
[AZ02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ02.png
[AZ03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ03.png
[AZ04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ04.png
[AZ05]: ./media/cache-java-spring-boot-initializer-with-redis-cache/AZ05.png

[SI01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI01.png
[SI02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI02.png
[SI03]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI03.png
[SI04]: ./media/cache-java-spring-boot-initializer-with-redis-cache/SI04.png

[RE01]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE01.png
[RE02]: ./media/cache-java-spring-boot-initializer-with-redis-cache/RE02.png
