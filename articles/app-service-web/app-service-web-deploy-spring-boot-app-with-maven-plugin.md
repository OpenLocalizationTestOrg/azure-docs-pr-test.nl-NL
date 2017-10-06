---
title: aaaHow toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een tooAzure Spring Boot-app
description: Meer informatie over hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een tooAzure Spring Boot-app.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een tooAzure Spring Boot-app

Hallo [Maven-invoegtoepassing voor Azure-Web-Apps](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) voor [Apache Maven](http://maven.apache.org/) biedt naadloze integratie van Azure App Service met Maven-projecten en stroomlijnt het Hallo-proces voor ontwikkelaars toodeploy web-apps tooAzure App Service.

Dit artikel wordt gedemonstreerd met behulp van Hallo Maven-invoegtoepassing voor Azure Web Apps toodeploy een voorbeeld Spring opstarten toepassing tooAzure App-Services.

> [!NOTE]
>
> Hallo Maven-invoegtoepassing voor Azure-Web-Apps is momenteel beschikbaar als een voorbeeld. Alleen FTP-publicatie wordt nu ondersteund, maar aanvullende functies zijn gepland voor toekomstige Hallo.
>

## <a name="prerequisites"></a>Vereisten

In de volgorde toocomplete Hallo stappen in deze zelfstudie moet u toohave Hallo volgende vereisten:

* Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].
* Hallo [Azure-opdrachtregelinterface (CLI)].
* Een up-to-date [Java Development Kit (JDK)], versie 1.7 of hoger.
* Apache van [Maven] bouwen tool (versie 3).
* Een [Git] client.

## <a name="clone-hello-sample-spring-boot-web-app"></a>Kloon Hallo voorbeeld Spring opstarten web-app

In dit gedeelte klonen van een voltooide Spring Boot-toepassing en lokaal testen.

1. Open een opdrachtprompt of een terminalvenster en maken van een lokale map toohold uw toepassing Spring opstarten en wijziging toothat directory; bijvoorbeeld:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- of--
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Kloon Hallo [Spring opstarten aan de slag] voorbeeldproject in Hallo directory die u hebt gemaakt; bijvoorbeeld:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Wijzigen van de directory toohello voltooid project. bijvoorbeeld:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Hallo JAR-bestand met behulp van Maven; bouwen bijvoorbeeld:
   ```shell
   mvn clean package
   ```

1. Wanneer het Hallo-web-app is gemaakt, start u Hallo web-app met behulp van Maven; bijvoorbeeld:
   ```shell
   mvn spring-boot:run
   ```

1. Hallo-web-app testen door te bladeren tooit lokaal via een webbrowser. U kunt bijvoorbeeld Hallo volgende opdracht als u curl beschikbaar hebt:
   ```shell
   curl http://localhost:8080
   ```

1. U ziet Hallo volgende bericht wordt weergegeven: **begroetingen vanaf Spring opstart!**

## <a name="create-an-azure-service-principal"></a>Een Azure-service-principal maken

In deze sectie maakt u een Azure service-principal die Hallo Maven-invoegtoepassing gebruikt bij het implementeren van uw web-app tooAzure.

1. Open een opdrachtprompt.

1. Meld u aan bij uw Azure-account met behulp van Hallo Azure CLI:
   ```shell
   az login
   ```
   Doe Hallo instructies toocomplete Hallo aanmelden.

1. Een Azure-service-principal maken:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Waar `uuuuuuuu` Hallo-gebruikersnaam en `pppppppp` Hallo wachtwoord voor de service-principal Hallo is.

1. Azure reageert met JSON dat lijkt op Hallo voorbeeld te volgen:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > U gebruikt Hallo waarden van deze JSON-antwoord als u uw web-app tooAzure hello Maven-invoegtoepassing toodeploy configureert. Hallo `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, en `tttttttt` tijdelijke aanduiding voor waarden die worden gebruikt in dit voorbeeld toomake deze eenvoudiger toomap deze waarden tootheir respectieve elementen bij het configureren van uw Maven `settings.xml` bestanden per Hallo naast sectie.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Uw Azure-service-principal voor Maven toouse configureren

In deze sectie kunt u Hallo waarden van uw Azure-service principal tooconfigure Hallo authentication Maven gebruikt bij het implementeren van uw web-app tooAzure gebruiken.

1. Open uw Maven `settings.xml` bestand in een teksteditor; dit bestand is mogelijk in een pad zoals Hallo volgen voorbeelden:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Toevoegen van uw Azure-service-principal-instellingen van de vorige sectie Hallo van deze zelfstudie toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Waar:
   Element | Beschrijving
   ---|---|---
   `<id>` | Hiermee geeft u een unieke naam op die Maven toolook van uw beveiligingsinstellingen worden gebruikt wanneer u uw web-app tooAzure implementeert.
   `<client>` | Hallo bevat `appId` waarde van uw service-principal.
   `<tenant>` | Hallo bevat `tenant` waarde van uw service-principal.
   `<key>` | Hallo bevat `password` waarde van uw service-principal.
   `<environment>` | Hallo doel-Azure-cloudomgeving, die definieert `AZURE` in dit voorbeeld. (Een volledige lijst met omgevingen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie)

1. Opslaan en sluiten Hallo *settings.xml* bestand.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>Optioneel: Uw pom.xml aanpassen voordat u uw web-app tooAzure implementeren

Open Hallo `pom.xml` bestand voor uw toepassing Spring opstarten in een teksteditor en zoek vervolgens Hallo `<plugin>` element voor `azure-webapp-maven-plugin`. Dit element moet eruitzien als Hallo voorbeeld te volgen:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Er zijn verschillende waarden die u voor Hallo Maven-invoegtoepassing wijzigen kunt en een gedetailleerde beschrijving in voor elk van deze elementen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie. Die wordt aangegeven, er zijn verschillende waarden die waard markeren in dit artikel zijn:

Element | Beschrijving
---|---|---
`<version>` | Hiermee geeft u de versie Hallo Hallo [Maven-invoegtoepassing voor Azure-Web-Apps]. Controleer Hallo-versie die worden vermeld in Hallo [Maven centrale opslagplaats](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure die u gebruikt Hallo meest recente versie.
`<authentication>` | Hiermee geeft u op Hallo verificatie-informatie voor Azure, die in dit voorbeeld bevat een `<serverId>` element met `azure-auth`; Maven maakt gebruik van die waarde toolook hello Azure-service-principal waarden in uw Maven *settings.xml* bestand, dat u hebt gedefinieerd in een eerdere sectie van dit artikel.
`<resourceGroup>` | Hiermee geeft u op Hallo doelresourcegroep, die `maven-plugin` in dit voorbeeld. Hallo resourcegroep wordt gemaakt tijdens de implementatie als deze niet al bestaat.
`<appName>` | Hiermee geeft u de doelnaam Hallo voor uw web-app. In dit voorbeeld is de naam van Hallo doel `maven-web-app-${maven.build.timestamp}`, waarbij hello `${maven.build.timestamp}` achtervoegsel wordt toegevoegd in dit voorbeeld tooavoid conflict. (Hallo tijdstempel is optioneel, kunt u een unieke tekenreeks voor de naam van de app Hallo.)
`<region>` | Hiermee geeft u de doelregio hello, die in dit voorbeeld is `westus`. (Een volledige lijst is in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.)
`<javaVersion>` | Hiermee geeft u Hallo Java runtime-versie voor uw web-app. (Een volledige lijst is in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.)
`<deploymentType>` | Hiermee geeft u een implementatietype voor uw web-app. Op dit moment alleen `ftp` wordt ondersteund, maar ondersteuning voor andere implementatietypen in ontwikkeling is.
`<resources>` | Hiermee geeft u resources en doel-doelen die Maven gebruikt bij het implementeren van uw web-app tooAzure. In dit voorbeeld twee `<resource>` elementen opgeven dat Maven Hallo JAR-bestand voor uw web-app en het Hallo inzetten *web.config* bestand uit Hallo Spring opstarten project.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Bouw en implementeer uw web-app tooAzure

Zodra u alle instellingen Hallo in Hallo voorgaande secties in dit artikel hebt geconfigureerd, u bent klaar toodeploy uw web-app tooAzure. toodo gebruik dus Hallo stappen te volgen:

1. Opnieuw samenstellen Hallo JAR-bestand met behulp van Maven, als u toohello wijzigingen aangebracht van Hallo-opdrachtprompt of terminalvenster die u eerder gebruikte *pom.xml* bestand; bijvoorbeeld:
   ```shell
   mvn clean package
   ```

1. Uw web-app tooAzure implementeren met behulp van Maven; bijvoorbeeld:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementeert uw web-app tooAzure; Als het Hallo-web-app niet al bestaat, wordt deze gemaakt.

Wanneer uw web-is geïmplementeerd, kunt u zich kunt toomanage deze met behulp van Hallo [Azure-portal].

* Uw web-app wordt weergegeven in **App Services**:

   ![Web-app die worden vermeld in Azure-portal App Services][AP01]

* En Hallo URL voor uw web-app wordt weergegeven in Hallo **overzicht** voor uw web-app:

   ![Hallo-URL voor uw web-app te bepalen][AP02]

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

Verschillende technologieën die worden beschreven in dit artikel, Zie voor meer informatie over Hallo Hallo artikelen te volgen:

* [Maven-invoegtoepassing voor Azure-Web-Apps]

* [Meld u bij tooAzure van hello Azure CLI](/azure/xplat-cli-connect)

* [Hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een beperkte app tooAzure voor Spring opstarten](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Een Azure-service-principal maken met Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Naslaginformatie over maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten aan de slag]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven-invoegtoepassing voor Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
