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
# <a name="how-tooconfigure-a-spring-boot-initializer-app-toouse-redis-cache"></a><span data-ttu-id="1b360-104">Hoe tooconfigure een versie die voorjaar opstarten initialisatiefunctie app toouse Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="1b360-104">How tooconfigure a Spring Boot Initializer app toouse Redis Cache</span></span>

## <a name="overview"></a><span data-ttu-id="1b360-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1b360-105">Overview</span></span>

<span data-ttu-id="1b360-106">Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="1b360-106">hello **[Spring Framework]** is an open-source solution which helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="1b360-107">Een van meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1b360-107">One of hello more-popular projects which is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="1b360-108">toohelp ontwikkelaars aan de slag met Spring opstarten, verschillende voorbeeld Spring opstarten pakketten zijn beschikbaar op <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="1b360-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="1b360-109">Bovendien toochoosing uit de lijst Hallo van basic Spring opstartinstallatiekopie projecten, hello  **[Spring Initializr]**  kunnen softwareontwikkelaars aan de slag met het maken van aangepaste Spring Boot-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1b360-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="1b360-110">Dit artikel begeleidt u bij het maken van een Redis-cache met behulp van Azure-portal met behulp van Hallo Hallo **Spring Initializr** toocreate een aangepaste toepassing, en maak vervolgens een Java-webtoepassing die zijn opgeslagen en opgehaald van de gegevens met uw Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="1b360-110">This article walks you through creating a Redis cache using hello Azure portal, then using hello **Spring Initializr** toocreate a custom application, and then creating a Java web application which stores and retrieves data using your Redis cache.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b360-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1b360-111">Prerequisites</span></span>

<span data-ttu-id="1b360-112">Hallo volgende vereiste onderdelen zijn vereist in de volgorde toofollow Hallo stappen in dit artikel:</span><span class="sxs-lookup"><span data-stu-id="1b360-112">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="1b360-113">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="1b360-113">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="1b360-114">Een [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), 1,7 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1b360-114">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="1b360-115">[Apache Maven](http://maven.apache.org/), versie 3.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1b360-115">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-a-redis-cache-on-azure"></a><span data-ttu-id="1b360-116">Een Redis-cache maken op Azure</span><span class="sxs-lookup"><span data-stu-id="1b360-116">Create a Redis cache on Azure</span></span>

1. <span data-ttu-id="1b360-117">Blader toohello Azure portal op <https://portal.azure.com/> en klikt u op Hallo-item voor **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="1b360-117">Browse toohello Azure portal at <https://portal.azure.com/> and click hello item for **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="1b360-119">Klik op **Database**, en klik vervolgens op **Redis-Cache**.</span><span class="sxs-lookup"><span data-stu-id="1b360-119">Click **Database**, and then click **Redis Cache**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="1b360-121">Op Hallo **nieuwe Redis-Cache** pagina, voert u Hallo **DNS-naam** voor uw cache geeft uw **abonnement**, **resourcegroep**,  **Locatie**, en **prijscategorie**.</span><span class="sxs-lookup"><span data-stu-id="1b360-121">On hello **New Redis Cache** page, enter hello **DNS name** for your cache, then specify your **Subscription**, **Resource group**, **Location**, and **Pricing tier**.</span></span> <span data-ttu-id="1b360-122">Wanneer u deze opties hebt opgegeven, klikt u op **maken** toocreate uw cache.</span><span class="sxs-lookup"><span data-stu-id="1b360-122">When you have specified these options, click **Create** toocreate your cache.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="1b360-124">Nadat uw cache is voltooid, ziet u het weergegeven in uw Azure **Dashboard**, evenals in Hallo **alle Resources**, en **Redis-Caches** pagina's.</span><span class="sxs-lookup"><span data-stu-id="1b360-124">Once your cache has been completed, you will see it listed on your Azure **Dashboard**, as well as under hello **All Resources**, and **Redis Caches** pages.</span></span> <span data-ttu-id="1b360-125">U kunt klikken op uw cache op een van deze locaties tooopen Hallo-pagina met eigenschappen voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="1b360-125">You can click on your cache on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="1b360-127">Wanneer het Hallo-pagina met Hallo-lijst van eigenschappen voor uw cache wordt weergegeven, klikt u op **toegangssleutels** en kopieer uw toegangssleutels voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="1b360-127">When hello page which contains hello list of properties for your cache is displayed, click **Access keys** and copy your access keys for your cache.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-custom-application-using-hello-spring-initializr"></a><span data-ttu-id="1b360-129">Een aangepaste toepassing maken met behulp Hallo Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="1b360-129">Create a custom application using hello Spring Initializr</span></span>

1. <span data-ttu-id="1b360-130">Te bladeren<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="1b360-130">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="1b360-131">U wilt opgeven dat toogenerate een **Maven** project met **Java**, Voer Hallo **groep** en **Aritifact** namen voor uw toepassing en klik vervolgens op Hallo-koppeling te**Switch toohello volledige versie** Hallo Spring Initializr.</span><span class="sxs-lookup"><span data-stu-id="1b360-131">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Aritifact** names for your application, and then click hello link too**Switch toohello full version** of hello Spring Initializr.</span></span>

   ![Basic Spring Initializr opties][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="1b360-133">Hallo Spring Initializr gebruikt Hallo **groep** en **Aritifact** namen toocreate Hallo pakketnaam; bijvoorbeeld: *com.contoso.myazuredemo*.</span><span class="sxs-lookup"><span data-stu-id="1b360-133">hello Spring Initializr will use hello **Group** and **Aritifact** names toocreate hello package name; for example: *com.contoso.myazuredemo*.</span></span>
   >

1. <span data-ttu-id="1b360-134">Schuif omlaag toohello **Web** sectie en het selectievakje in voor Hallo **Web**, schuif naar beneden toohello **NoSQL** sectie en het selectievakje in voor Hallo **Redis**, schuif vervolgens toohello onder aan Hallo pagina en klik op Hallo te**genereren Project**.</span><span class="sxs-lookup"><span data-stu-id="1b360-134">Scroll down toohello **Web** section and check hello box for **Web**, then scroll down toohello **NoSQL** section and check hello box for **Redis**, then scroll toohello bottom of hello page and click hello button too**Generate Project**.</span></span>

   ![Opties voor volledige Spring Initializr][SI02]

1. <span data-ttu-id="1b360-136">Wanneer u wordt gevraagd, downloadpad Hallo project tooa op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="1b360-136">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Aangepaste Spring Boot-project downloaden][SI03]

1. <span data-ttu-id="1b360-138">Nadat u hebt uitgepakt Hallo-bestanden op uw lokale systeem, zal uw aangepaste Spring Boot-toepassing gereed is voor het bewerken van zijn.</span><span class="sxs-lookup"><span data-stu-id="1b360-138">After you have extracted hello files on your local system, your custom Spring Boot application will be ready for editing.</span></span>

   ![Aangepaste Spring project opstartbestanden][SI04]

## <a name="configure-your-custom-spring-boot-toouse-your-redis-cache"></a><span data-ttu-id="1b360-140">Uw aangepaste Spring Boot toouse uw Redis-Cache configureren</span><span class="sxs-lookup"><span data-stu-id="1b360-140">Configure your custom Spring Boot toouse your Redis Cache</span></span>

1. <span data-ttu-id="1b360-141">Zoek Hallo *application.properties* bestand in Hallo *resources* map van uw app of Hallo-bestand maken als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="1b360-141">Locate hello *application.properties* file in hello *resources* directory of your app, or create hello file if it does not already exist.</span></span>

   ![Hallo application.properties bestand gevonden][RE01]

1. <span data-ttu-id="1b360-143">Open Hallo *application.properties* bestand in een teksteditor en Hallo voorbeeldwaarden vervangen door Hallo toepasselijke eigenschappen uit uw cache Hallo volgende toohello regels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1b360-143">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties from your cache:</span></span>

   ```yaml
   # Specify hello DNS URI of your Redis cache.
   spring.redis.host=myspringbootcache.redis.cache.windows.net

   # Specify hello port for your Redis cache.
   spring.redis.port=6380

   # Specify hello access key for your Redis cache.
   spring.redis.password=57686f6120447564652c2049495320526f636b73=
   ```

   ![Hallo application.properties bestand bewerken][RE02]

1. <span data-ttu-id="1b360-145">Opslaan en sluiten Hallo *application.properties* bestand.</span><span class="sxs-lookup"><span data-stu-id="1b360-145">Save and close hello *application.properties* file.</span></span>

1. <span data-ttu-id="1b360-146">Maak een map met de naam *controller* onder Hallo bronmap voor het pakket; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1b360-146">Create a folder named *controller* under hello source folder for your package; for example:</span></span>

   `C:\SpringBoot\myazuredemo\src\main\java\com\contoso\myazuredemo\controller`

   <span data-ttu-id="1b360-147">-of-</span><span class="sxs-lookup"><span data-stu-id="1b360-147">-or-</span></span>

   `/users/example/home/myazuredemo/src/main/java/com/contoso/myazuredemo/controller`

1. <span data-ttu-id="1b360-148">Maak een nieuw bestand met de naam *HelloController.java* in Hallo *controller* map.</span><span class="sxs-lookup"><span data-stu-id="1b360-148">Create a new file named *HelloController.java* in hello *controller* folder.</span></span> <span data-ttu-id="1b360-149">Hallo-bestand openen in een teksteditor en voeg toe Hallo code tooit te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b360-149">Open hello file in a text editor and add hello following code tooit:</span></span>

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
   
   <span data-ttu-id="1b360-150">Hier moet u tooreplace `com.contoso.myazuredemo` met Hallo pakketnaam voor uw project.</span><span class="sxs-lookup"><span data-stu-id="1b360-150">Where you will need tooreplace `com.contoso.myazuredemo` with hello package name for your project.</span></span>

1. <span data-ttu-id="1b360-151">Opslaan en sluiten Hallo *HelloController.java* bestand.</span><span class="sxs-lookup"><span data-stu-id="1b360-151">Save and close hello *HelloController.java* file.</span></span>

1. <span data-ttu-id="1b360-152">Uw toepassing Spring opstarten met Maven bouwen en uitvoeren. bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1b360-152">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn clean package
   mvn spring-boot:run
   ```

1. <span data-ttu-id="1b360-153">Hallo web-app testen door te bladeren toohttp://localhost:8080 met een webbrowser, of gebruik de syntaxis Hallo zoals Hallo na voorbeeld hebt u curl beschikbaar:</span><span class="sxs-lookup"><span data-stu-id="1b360-153">Test hello web app by browsing toohttp://localhost:8080 using a web browser, or use hello syntax like hello following example if you have curl available:</span></span>

   ```shell
   curl http://localhost:8080
   ```

   <span data-ttu-id="1b360-154">U ziet Hallo "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="1b360-154">You should see hello "Hello World!"</span></span> <span data-ttu-id="1b360-155">bericht ontvangen van uw voorbeeld-domeincontroller die wordt weergegeven, die dynamisch worden opgehaald uit de Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="1b360-155">message from your sample controller displayed, which is being retrieved dynamically from your Redis cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b360-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1b360-156">Next steps</span></span>

<span data-ttu-id="1b360-157">Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1b360-157">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="1b360-158">Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="1b360-158">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="1b360-159">Een versie die voorjaar opstarten toepassing uitvoert in een Kubernetes Cluster in hello Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="1b360-159">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="1b360-160">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="1b360-160">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="1b360-161">Zie voor meer informatie over het ophalen van de slag met Redis-Cache met behulp van Java in Azure, [hoe toouse Azure Redis-Cache met behulp van Java][Redis Cache with Java].</span><span class="sxs-lookup"><span data-stu-id="1b360-161">For more information about getting started using Redis Cache with Java on Azure, see [How toouse Azure Redis Cache with Java][Redis Cache with Java].</span></span>

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
