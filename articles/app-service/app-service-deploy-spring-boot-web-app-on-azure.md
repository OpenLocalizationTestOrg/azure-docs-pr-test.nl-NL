---
title: aaaDeploy een versie die voorjaar opstarten toepassing toohello Azure App Service | Microsoft Docs
description: Deze zelfstudie leidt ontwikkelaars via Hallo stappen toodeploy Hallo Spring opstarten aan de slag web app tooAzure App Service.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren

Hallo  **[Spring Framework]**  is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken en een meer populaire Hallo-projecten die is gebaseerd op dat platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.

Deze zelfstudie leert u echter Hallo voorbeeld Spring opstarten aan de slag web-app maken en te implementeren[Azure App Service].

### <a name="prerequisites"></a>Vereisten

In de volgorde toocomplete Hallo stappen in deze zelfstudie hebt u toohave Hallo volgende nodig:

* Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].
* Een up-to-date [Java Developer Kit (JDK)].
* Apache van [Maven] bouwen tool (versie 3).
* Een [Git] client.

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Hallo Spring opstarten aan de slag web-app maken

Hallo begeleidt volgt u stapsgewijs door Hallo stappen die zijn vereist toocreate een eenvoudige webtoepassing voor Spring opstarten en lokaal testen.

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

1. Kloon Hallo [Spring opstarten aan de slag] voorbeeldproject in Hallo directory die u zojuist hebt gemaakt, bijvoorbeeld:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Wijzigen van de directory toohello voltooid project. bijvoorbeeld:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:
   ```
   mvn package
   ```

1. Zodra het Hallo-web-app is gemaakt, directory toohello JAR-bestand te wijzigen en Hallo web-app starten bijvoorbeeld:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Hallo web-app testen door te bladeren toohttp://localhost:8080 met een webbrowser, of gebruik de syntaxis Hallo zoals Hallo na voorbeeld hebt u curl beschikbaar:
   ```
   curl http://localhost:8080
   ```

1. U ziet Hallo volgende bericht wordt weergegeven: **begroetingen vanaf Spring opstart!**

   ![Voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Maken van een Azure-web-app voor gebruik met Java

Hallo stappen te volgen wordt stapsgewijs Hallo stappen toocreate een Azure-Web-App, Hallo vereiste instellingen configureren voor Java en uw FTP-referenties configureren.

1. Blader toohello [Azure-portal] en zich aanmelden.

1. Nadat u hebt geregistreerd bij uw account op Hallo Azure-portal, klikt u op Hallo menupictogram voor **App Services**:
   
   ![Azure Portal][AZ01]

1. Wanneer Hallo **App Services** pagina wordt weergegeven, klikt u op **+ toevoegen** toocreate een nieuwe App Service.

   ![App Service maken][AZ02]

1. Wanneer Hallo lijst met sjablonen voor web-app wordt weergegeven, klikt u op de koppeling Hallo voor Hallo basic Microsoft Web-App.

   ![Sjablonen voor Web-App][AZ03]

1. Wanneer Hallo informatiepagina voor Hallo Web-App-sjabloon wordt weergegeven, klikt u op **maken**.

   ![Web-app maken][AZ04]

1. Geef een unieke naam voor uw web-app en geef eventuele aanvullende instellingen en vervolgens **maken**.

   ![Instellingen voor Web-App maken][AZ05]

1. Nadat uw web-app is gemaakt, klikt u op Hallo menupictogram voor **App Services**, en klik vervolgens op uw nieuwe web-app:

   ![Lijst met Web-Apps][AZ06]

1. Wanneer uw web-app wordt weergegeven, geeft u Hallo Java-versie via Hallo stappen te volgen:

   a. Klik op Hallo **toepassingsinstellingen** menu-item.

   b. Kies **Java 8** voor Hallo Java-versie.

   c. Kies **nieuwste** voor Hallo secundaire Java-versie.

   d. Kies **nieuwste Tomcat 8.5** voor Hallo webcontainer. (Deze container niet daadwerkelijk wordt gebruikt; Azure gebruikt Hallo container van uw toepassing Spring opstarten.)

   e. Klik op **Opslaan**.

   ![Toepassingsinstellingen][AZ07]

1. Geef uw FTP-implementatiereferenties met behulp van Hallo stappen te volgen:

   a. Klik op Hallo **Implementatiereferenties** menu-item.

   b. Geef uw gebruikersnaam en wachtwoord.

   c. Klik op **Opslaan**.

   ![Geef referenties voor implementatie][AZ08]

1. De FTP-verbindingsgegevens ophalen met behulp van Hallo stappen te volgen:

   a. Klik op Hallo **Implementatiereferenties** menu-item.

   b. Uw volledige FTP-gebruikersnaam en de URL kopiëren en opslaan voor de volgende sectie Hallo van deze zelfstudie.

   ![FTP-URL en referenties][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Uw tooAzure Spring opstarten web-app implementeren

Hallo stappen te volgen begeleidt u stapsgewijs door Hallo stappen toodeploy uw tooAzure Spring opstarten web-app.

1. Open een teksteditor zoals Kladblok van Windows op Hallo volgende tekst naar een nieuw document plakken en Hallo bestand opslaan als *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. Nadat u hebt opgeslagen Hallo *web.config* tooyour bestandssysteem, tooyour web-app via de FTP-met Hallo-URL, gebruikersnaam en wachtwoord van de voorgaande sectie van deze zelfstudie Hallo verbinden. Bijvoorbeeld:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Wijziging Hallo externe map toohello hoofdmap van uw web-app (die is op */site/wwwroot*), kopieert u Hallo JAR-bestand van uw toepassing Spring opstarten en Hallo *web.config* van eerder. Bijvoorbeeld:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. Nadat u uw JAR hebt geïmplementeerd en *web.config* bestanden tooyour web-app, moet u toorestart na uw web-app met behulp van hello Azure-portal:

   ![][AZ10]

1. Hallo web-app testen door te bladeren tooyour van web-app-URL met een webbrowser, of gebruik de syntaxis Hallo zoals Hallo na voorbeeld hebt u curl beschikbaar:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. U ziet Hallo volgende bericht wordt weergegeven: **begroetingen vanaf Spring opstart!**

   ![Voorbeeld-App bladeren][SB02]

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van opstarten Spring toepassingen in Azure Hallo artikelen te volgen:

* [Een toepassing Spring opstarten op Linux in hello Azure Container Service implementeren](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Een toepassing Spring opstarten op een Kubernetes Cluster in hello Azure Container Service implementeren](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].

Zie voor meer informatie over depoying web apps tooAzure met FTP, [implementeren van uw app tooAzure App Service met behulp van FTP/S].

Zie voor meer informatie over Hallo Spring Boot-voorbeeldproject [Spring opstarten aan de slag].

Zie voor meer informatie over aan de slag met uw eigen toepassingen Spring opstarten, Hallo **Spring Initializr** op https://start.spring.io/.

Zie voor meer informatie over het configureren van aanvullende instellingen voor uw web-app [web-apps configureren in Azure App Service].

<!-- URL List -->

[Azure App Service]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[web-apps configureren in Azure App Service]: /azure/app-service-web/web-sites-configure
[implementeren van uw app tooAzure App Service met behulp van FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten aan de slag]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
