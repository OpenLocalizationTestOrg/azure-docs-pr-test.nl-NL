---
title: aaaHow toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een versie die voorjaar Boot-app in Azure Container register tooAzure App Service
description: Deze zelfstudie leert u echter Hallo stappen toodeploy een versie die voorjaar Boot-toepassing in Azure Container register tooAzure tooAzure App Service met behulp van een Maven-invoegtoepassing.
services: 
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
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Hoe toouse hello Maven-invoegtoepassing voor Azure Web Apps toodeploy een versie die voorjaar Boot-app in Azure Container register tooAzure App Service

Hallo  **[Spring Framework]**  is een populaire open-source framework waarmee ontwikkelaars van Java web, mobiel en API-toepassingen maken. In deze zelfstudie wordt een voorbeeld-app gemaakt met behulp van [Spring Boot], een conventie voor gestuurde benadering voor het gebruik van Spring tooget snel aan de slag.

In dit artikel laat zien hoe een voorbeeld Spring opstarten toepassing tooAzure Container register toodeploy, en gebruik hello Maven-invoegtoepassing voor Azure Web Apps toodeploy uw toepassing tooAzure App Service.

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
* Een [Docker] client.

> [!NOTE]
>
> Vanwege toohello virtualisatie vereisten van deze zelfstudie, kan niet u Hallo stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Kloon Hallo voorbeeld Spring opstarten op Docker-web-app

In dit gedeelte klonen van een beperkte Spring Boot-toepassing en lokaal testen.

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

1. Kloon Hallo [Spring opstarten op het Docker aan de slag] voorbeeldproject in Hallo directory die u hebt gemaakt; bijvoorbeeld:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. Wijzigen van de directory toohello voltooid project. bijvoorbeeld:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. U ziet Hallo volgende bericht wordt weergegeven: **Hallo Docker wereld**

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-service-principal"></a>Een Azure-service-principal maken

In deze sectie maakt u een Azure service-principal die Hallo Maven-invoegtoepassing gebruikt bij het implementeren van uw tooAzure container.

1. Open een opdrachtprompt.

1. Meld u aan bij uw Azure-account met behulp van Hallo Azure CLI:
   ```azurecli
   az login
   ```
   Doe Hallo instructies toocomplete Hallo aanmelden.

1. Een Azure-service-principal maken:
   ```azurecli
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
   > U gebruikt Hallo waarden van deze JSON-antwoord als u uw tooAzure container Hallo Maven-invoegtoepassing toodeploy configureert. Hallo `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, en `tttttttt` tijdelijke aanduiding voor waarden die worden gebruikt in dit voorbeeld toomake deze eenvoudiger toomap deze waarden tootheir respectieve elementen bij het configureren van uw Maven `settings.xml` bestanden per Hallo naast sectie.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Maken van een Azure Container Registry hello Azure CLI gebruiken

1. Open een opdrachtprompt.

1. Meld u bij tooyour Azure-account:
   ```azurecli
   az login
   ```

1. Maak een resourcegroep voor hello Azure-resources die gaat u in dit artikel:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Vervang `wingtiptoysresources` in dit voorbeeld met een unieke naam voor de resourcegroep.

1. Maak een register persoonlijke Azure-container in Hallo resourcegroep voor uw app Spring opstarten: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Vervang `wingtiptoysregistry` in dit voorbeeld met een unieke naam voor de container-register.

1. Hallo-wachtwoord voor de container-register worden opgehaald:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure reageert met je wachtwoord; bijvoorbeeld:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Uw Azure-container register en de Azure service principal tooyour Maven-instellingen toevoegen

1. Open uw Maven `settings.xml` bestand in een teksteditor; dit bestand is mogelijk in een pad zoals Hallo volgen voorbeelden:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Uw toegang tot Azure Container registerinstellingen toevoegen uit de vorige sectie Hallo van dit artikel toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Waar:
   Element | Beschrijving
   ---|---|---
   `<id>` | Hallo-naam van het register persoonlijke Azure-container bevat.
   `<username>` | Hallo-naam van het register persoonlijke Azure-container bevat.
   `<password>` | Hallo wachtwoord dat u hebt opgehaald in de vorige sectie Hallo van dit artikel bevat.

1. Toevoegen van uw Azure-service-principal-instellingen in een eerder gedeelte van dit artikel toohello `<servers>` verzameling in hello *settings.xml* bestand; bijvoorbeeld:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Uw Docker-container-installatiekopie maken en dit tooyour Azure container register doorgeven

1. Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten (bijvoorbeeld) "*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*'), en open Hallo *pom.xml* het bestand met een teksteditor.

1. Update Hallo `<properties>` verzameling in hello *pom.xml* -bestand met Hallo aanmelding serverwaarde voor uw Azure-Container register uit de vorige sectie Hallo van deze zelfstudie; bijvoorbeeld:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Waar:
   Element | Beschrijving
   ---|---|---
   `<azure.containerRegistry>` | Hiermee geeft u Hallo-naam van het register persoonlijke Azure-container.
   `<docker.image.prefix>` | Hallo-URL van het register persoonlijke Azure-container, die is afgeleid door toe te voegen '. azurecr.io ' toohello-naam van het register privé-container.

1. Controleer `<plugin>` voor Hallo Docker-invoegtoepassing in uw *pom.xml* bestand bevat de juiste eigenschappen Hallo voor Hallo-server en het register aanmeldingsnaam van de vorige stap Hallo in deze zelfstudie. Bijvoorbeeld:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Waar:
   Element | Beschrijving
   ---|---|---
   `<serverId>` | Hiermee geeft u Hallo-eigenschap met de naam van het register persoonlijke Azure-container.
   `<registryUrl>` | Hiermee geeft u Hallo-eigenschap die Hallo-URL van het register persoonlijke Azure-container bevat.

1. Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten en uitvoeren na opdracht toorebuild Hallo toepassing hello en push Hallo container tooyour Azure container register:

   ```
   mvn package docker:build -DpushImage 
   ```

1. Optioneel: Bladeren toohello [Azure-portal] en controleer of er een installatiekopie van Docker-container met de naam **gs-spring-boot-docker** in het register van de container.

   ![Controleer of de container in Azure-portal][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Uw pom.xml aanpassen en vervolgens te bouwen en implementeren van uw tooAzure container

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Er zijn verschillende waarden die u voor Hallo Maven-invoegtoepassing wijzigen kunt en een gedetailleerde beschrijving in voor elk van deze elementen is beschikbaar in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie. Die wordt aangegeven, er zijn verschillende waarden die waard markeren in dit artikel zijn:

Element | Beschrijving
---|---|---
`<version>` | Hiermee geeft u de versie Hallo Hallo [Maven-invoegtoepassing voor Azure-Web-Apps]. Controleer Hallo-versie die worden vermeld in Hallo [Maven centrale opslagplaats](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure die u gebruikt Hallo meest recente versie.
`<authentication>` | Hiermee geeft u op Hallo verificatie-informatie voor Azure, die in dit voorbeeld bevat een `<serverId>` element met `azure-auth`; Maven maakt gebruik van die waarde toolook hello Azure-service-principal waarden in uw Maven *settings.xml* bestand, dat u hebt gedefinieerd in een eerdere sectie van dit artikel.
`<resourceGroup>` | Hiermee geeft u op Hallo doelresourcegroep, die `wingtiptoysresources` in dit voorbeeld. Hallo resourcegroep wordt gemaakt tijdens de implementatie als deze niet al bestaat.
`<appName>` | Hiermee geeft u de doelnaam Hallo voor uw web-app. In dit voorbeeld is de naam van Hallo doel `maven-linux-app-${maven.build.timestamp}`, waarbij hello `${maven.build.timestamp}` achtervoegsel wordt toegevoegd in dit voorbeeld tooavoid conflict. (Hallo tijdstempel is optioneel, kunt u een unieke tekenreeks voor de naam van de app Hallo.)
`<region>` | Hiermee geeft u de doelregio hello, die in dit voorbeeld is `westus`. (Een volledige lijst is in Hallo [Maven-invoegtoepassing voor Azure-Web-Apps] documentatie.)
`<containerSettings>` | Hiermee geeft u Hallo-eigenschappen die Hallo naam en de URL van de container bevatten.
`<appSettings>` | Hiermee geeft u een unieke instellingen voor Maven toouse bij het implementeren van uw web-app tooAzure. In dit voorbeeld wordt een `<property>` element bevat een naam/waarde-paar van onderliggende elementen die Hallo-poort voor uw app opgeven.

> [!NOTE]
>
> Hallo instellingen toochange Hallo-poortnummer in dit voorbeeld zijn alleen nodig als u poort Hallo van Hallo standaardwaarde wijzigt.
>

1. Opnieuw samenstellen Hallo JAR-bestand met behulp van Maven, als u toohello wijzigingen aangebracht van Hallo-opdrachtprompt of terminalvenster die u eerder gebruikte *pom.xml* bestand; bijvoorbeeld:
   ```shell
   mvn clean package
   ```

1. Uw web-app tooAzure implementeren met behulp van Maven; bijvoorbeeld:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven implementeert uw web-app tooAzure; Als het Hallo-web-app niet al bestaat, wordt deze gemaakt.

> [!NOTE]
>
> Als Hallo regio die u in Hallo opgeeft `<region>` element van uw *pom.xml* bestand beschikt niet over voldoende beschikbare servers wanneer u de implementatie start, ziet u mogelijk een foutbericht vergelijkbaar toohello voorbeeld te volgen:
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> Als dit gebeurt, kunt u dat een andere regio en Voer Hallo Maven-opdracht toodeploy uw toepassing.
>
>

Wanneer uw web-is geïmplementeerd, kunt u zich kunt toomanage deze met behulp van Hallo [Azure-portal].

* Uw web-app wordt weergegeven in **App Services**:

   ![Web-app die worden vermeld in Azure-portal App Services][AP01]

* En Hallo URL voor uw web-app wordt weergegeven in Hallo **overzicht** voor uw web-app:

   ![Hallo-URL voor uw web-app te bepalen][AP02]

## <a name="next-steps"></a>Volgende stappen

Verschillende technologieën die worden beschreven in dit artikel, Zie voor meer informatie over Hallo Hallo artikelen te volgen:

* [Maven-invoegtoepassing voor Azure-Web-Apps]

* [Meld u bij tooAzure van hello Azure CLI](/azure/xplat-cli-connect)

* [Een Azure-service-principal maken met Azure CLI 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Naslaginformatie over maven](https://maven.apache.org/settings.html)

* [Maven docker-invoegtoepassing]

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure-portal]: https://portal.azure.com/
[Maven-invoegtoepassing voor Azure-Web-Apps]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Maven docker-invoegtoepassing]: https://github.com/spotify/docker-maven-plugin
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
