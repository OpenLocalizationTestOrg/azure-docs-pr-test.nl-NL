---
title: een versie die voorjaar opstarten Web-App op Linux in Azure Container Service aaaDeploy | Microsoft Docs
description: Deze zelfstudie wordt u echter Hallo stappen toodeploy een toepassing Spring opstarten als een Linux-web-app in Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Een toepassing Spring opstarten op Linux in hello Azure Container Service implementeren

Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.

**[Docker]**  is open source-oplossingen waarmee ontwikkelaars automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.

In deze zelfstudie leert u met behulp van Docker toodevelop en implementeren van een versie die voorjaar opstarten toepassing tooa Linux-host in Hallo [Azure Container Service (ACS)].

## <a name="prerequisites"></a>Vereisten

In de volgorde toocomplete Hallo stappen in deze zelfstudie moet u toohave Hallo volgende vereisten:

* Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].
* Hallo [Azure-opdrachtregelinterface (CLI)].
* Een up-to-date [Java Developer Kit (JDK)].
* Apache van [Maven] bouwen tool (versie 3).
* Een [Git] client.
* Een [Docker] client.

> [!NOTE]
>
> Vanwege toohello virtualisatie vereisten van deze zelfstudie, kan niet u Hallo stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Hallo Spring opstarten op Docker aan de slag web-app maken

Hallo doorlopen volgt u Hallo stappen die vereist toocreate een eenvoudige webtoepassing voor Spring opstarten en lokaal testen.

1. Open een opdrachtprompt en maken van een lokale map toohold uw toepassing en de wijziging toothat directory; bijvoorbeeld:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- of--
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Kloon Hallo [Spring opstarten op het Docker aan de slag] voorbeeldproject in Hallo directory die u hebt gemaakt; bijvoorbeeld:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Wijzigen van de directory toohello voltooid project. bijvoorbeeld:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:
   ```
   mvn package
   ```

1. Zodra het Hallo-web-app is gemaakt, verandert directory toohello `target` directory waar Hallo JAR-bestand zich bevindt en Hallo web-app starten bijvoorbeeld:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Hallo-web-app testen door te bladeren tooit lokaal via een webbrowser. Bijvoorbeeld, als u curl beschikbaar en u geconfigureerd Hallo Tomcat-server toorun op poort 80:
   ```
   curl http://localhost
   ```

1. U ziet Hallo volgende bericht wordt weergegeven: **Hello Docker World!**

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Maak een Azure Container register toouse als een persoonlijke Docker-register

Hallo doorlopen volgende stappen Hallo toocreate met Azure portal een Azure Container Registry gebruiken.

> [!NOTE]
>
> Als u wilt dat toouse hello Azure CLI in plaats van hello Azure-portal, stappen Hallo in [maken van een persoonlijke Docker-container register met behulp van Azure CLI 2.0 Hallo](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Blader toohello [Azure-portal] en meld u aan.

   Wanneer u bent aangemeld in tooyour-account op Hallo Azure-portal, u kunt stappen Hallo in Hallo [maken van een persoonlijke Docker-container register hello Azure-portal met] artikel, dat in de volgende stappen uit voor Hallo Hallo zijn paraphrased verjaardagen praktische.

1. Klik op Hallo menupictogram voor **+ nieuw**, klikt u vervolgens op **Containers**, en klik vervolgens op **Azure Container register**.
   
   ![Maak een nieuwe Azure-Container register][AR01]

1. Wanneer de informatiepagina Hallo voor hello Azure Container register sjabloon wordt weergegeven, klikt u op **maken**. 

   ![Maak een nieuwe Azure-Container register][AR02]

1. Wanneer Hallo **maken container register** pagina wordt weergegeven, voert u uw **naam van Routeringsregister** en **resourcegroep**, kies **inschakelen** voor Hallo **gebruiker met beheerdersrechten**, en klik vervolgens op **maken**.

   ![Azure-Container registerinstellingen configureren][AR03]

1. Zodra het register van de container is gemaakt, gaat u tooyour container register in hello Azure-portal en klik vervolgens op **toegangstoetsen**. Let op het Hallo-gebruikersnaam en wachtwoord voor de volgende stappen Hallo.

   ![Azure Container toegang registersleutels][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Uw toegang tot Azure Container registersleutels Maven toouse configureren

1. Navigeer toohello configuratiemap voor uw installatie Maven en open Hallo *settings.xml* bestand met een teksteditor.

1. Uw toegang tot Azure Container registerinstellingen toevoegen uit de vorige sectie Hallo van deze zelfstudie toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten (bijvoorbeeld: '*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker / volledige*'), en open Hallo *pom.xml* bestand met een teksteditor.

1. Update Hallo `<properties>` verzameling in hello *pom.xml* -bestand met Hallo aanmelding serverwaarde voor uw Azure-Container register uit de vorige sectie Hallo van deze zelfstudie; bijvoorbeeld:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Update Hallo `<plugins>` verzameling in hello *pom.xml* bestand die Hallo `<plugin>` Hallo aanmelding adres en het register servernaam voor uw Azure-Container register uit de vorige sectie Hallo van deze zelfstudie bevat. Bijvoorbeeld:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten en uitgevoerd na opdracht toorebuild Hallo toepassing hello en push Hallo container tooyour Azure Container register:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Wanneer u uw tooAzure Docker-container worden gepusht, verschijnt er een foutbericht weergegeven dat vergelijkbaar tooone van Hallo volgen, ondanks dat de Docker-container is gemaakt:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Als dit gebeurt, moet u mogelijk toosign in tooyour Azure-account van Hallo Docker-opdrachtregel; bijvoorbeeld:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> U kunt vervolgens de container push vanaf de opdrachtregel Hallo; bijvoorbeeld:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Een web-app maken in Linux op Azure App Service met behulp van de installatiekopie van de container

1. Blader toohello [Azure-portal] en meld u aan.

1. Klik op Hallo menupictogram voor **+ nieuw**, klikt u vervolgens op **Web en mobiel**, en klik vervolgens op **Web-App op Linux**.
   
   ![Een nieuwe WebApp maken in hello Azure-portal][LX01]

1. Wanneer Hallo **Web-App op Linux** pagina wordt weergegeven, voert u Hallo volgende informatie:

   a. Geef een unieke naam voor Hallo **appnaam**; bijvoorbeeld: '*wingtiptoyslinux*. "

   b. Kies uw **abonnement** uit de vervolgkeuzelijst Hallo.

   c. Kies een bestaande **resourcegroep**, of geef een naam toocreate een nieuwe resourcegroep.

   d. Klik op **configureren container** en voer de volgende informatie Hallo:

      * Kies **persoonlijke register**.

      * **Installatiekopie en optionele tag**: Geef de containernaam van uw van eerder; bijvoorbeeld: '*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*'

      * **Server-URL**: Geef de URL van het register van eerder; bijvoorbeeld: '*https://wingtiptoysregistry.azurecr.io*'

      * **Gebruikersnaam voor aanmelding** en **wachtwoord**: Geef de referenties van uw **toegangstoetsen** die u gebruikt in de vorige stappen.
   
   e. Nadat u alle Hallo boven de gegevens hebt ingevoerd, klikt u op **OK**.

   ![Instellingen voor web-app configureren][LX02]

1. Klik op **Create**.

> [!NOTE]
>
> Azure Internet aanvragen tooembedded Tomcat-server die wordt uitgevoerd op de standaardpoorten Hallo van 80 of 8080 automatisch toegewezen. Als u uw ingesloten toorun van de Tomcat-server op een aangepaste poort geconfigureerd, moet u tooadd een omgeving variabele tooyour web-app die Hallo-poort voor de ingesloten Tomcat-server definieert. toodo gebruik dus Hallo stappen te volgen:
>
> 1. Blader toohello [Azure-portal] en meld u aan.
> 
> 2. Klik op het pictogram voor Hallo **App Services**. (Zie artikel #1 in onderstaande afbeelding voor Hallo.)
>
> 3. Selecteer uw web-app in Hallo-lijst. (Item #2 in onderstaande afbeelding voor Hallo.)
>
> 4. Klik op **toepassingsinstellingen**. (Item #3 in onderstaande afbeelding voor Hallo.)
>
> 5. In Hallo **appinstellingen** sectie, het toevoegen van een nieuwe omgevingsvariabele met de naam **poort** en voer het nummer van uw aangepaste poort voor Hallo-waarde. (Item #4 in onderstaande afbeelding voor Hallo.)
>
> 6. Klik op **Opslaan**. (Item #5 in onderstaande afbeelding voor Hallo.)
>
> ![Opslaan van een aangepast poortnummer in hello Azure-portal][LX03]
>

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:

* [Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Een toepassing Spring opstarten op een Kubernetes Cluster in hello Azure Container Service implementeren](container-service-deploy-spring-boot-app-on-kubernetes.md)

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

Zie voor meer informatie over Hallo Spring opstarten op Docker-voorbeeldproject [Spring opstarten op het Docker aan de slag].

Zie voor meer informatie over aan de slag met uw eigen toepassingen Spring opstarten, Hallo **Spring Initializr** op https://start.spring.io/.

Zie voor meer informatie over het aan de slag met het maken van een eenvoudige Spring Boot-toepassing hello Spring Initializr op https://start.spring.io/.

Zie voor meer voorbeelden van hoe toouse aangepaste Docker met Azure afbeeldingen [met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux].

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[maken van een persoonlijke Docker-container register hello Azure-portal met]: /azure/container-registry/container-registry-get-started-portal
[met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
