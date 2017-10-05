---
title: Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ | Microsoft Docs
description: Informatie over het publiceren van een web-app naar Microsoft Azure als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ.
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 06/21/2017
ms.author: robmcm
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a>Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ

De [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een van de meer populaire projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.

[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.

Deze zelfstudie leert u de stappen voor het implementeren van een toepassing Spring opstarten als een Docker-container met Microsoft Azure met behulp van de Azure-Toolkit voor IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a>Kloon de standaard Spring Boot Docker-opslagplaats

De volgende stappen maakt u via de Spring Boot Docker-opslagplaats met behulp van IntelliJ klonen. Als u wilt een opdrachtregel te gebruiken, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].

1. Open IntelliJ.

1. Selecteer op het welkomstscherm van de **GitHub** optie in de **uitchecken uit versiebeheer** lijst.

   ![GitHub-optie voor versiebeheer][CL01]

1. Geef uw referenties als u wordt gevraagd om aan te melden.

   * Als u een gebruikersnaam en wachtwoord voor aanmelding bij GitHub:

      ![In het dialoogvenster voor het invoeren van GitHub-gebruikersnaam en wachtwoord][CL02a]

   * Als u een token gebruikt voor aanmelding bij GitHub:

      ![In het dialoogvenster voor het invoeren van een GitHub-token][CL02b]

1. Voer **https://github.com/spring-guides/gs-spring-boot-docker.git** opgeven voor de URL van de opslagplaats, uw lokale pad en de mapgegevens en klik vervolgens op **kloon**.

   ![Dialoogvenster kloon-opslagplaats][CL03]

1. Wanneer u wordt gevraagd om een IntelliJ-project te maken, selecteert u **Nee**.

   ![Weigeren een IntelliJ-project maken][CL04]

1. Klik op de welkomstpagina op **Project importeren**.

   ![Het project importeren][CL05]

1. Zoek het pad waar u de opslagplaats Spring opstarten gekloond, selecteert u de **voltooid** map onder de hoofdmap en klik vervolgens op **OK**.

   ![Selecteer een map voor importeren][CL06]

1. Wanneer u wordt gevraagd, selecteert u **project maken van bestaande bronnen**.

   ![Optie voor het maken van een project van bestaande bronnen][CL07]

1. Geef de projectnaam van uw of accepteer de standaardinstelling, controleert u het juiste pad naar de **voltooid** map en klik vervolgens op **volgende**.

   ![Geef de naam van het project][CL08]

1. Alle mappen voor het importeren van aanpassen en klik vervolgens op **volgende**.

   ![Kies de mappen][CL09]

1. Bekijk de bibliotheken om te importeren en klik vervolgens op **volgende**.

   ![Bekijk de project-bibliotheken][CL10]

1. Structuur van de module bekijken en klik vervolgens op **volgende**.

   ![Bekijk de modulestructuur][CL11]

1. Geef uw JDK en klik vervolgens op **volgende**.

   ![Geef een JDK][CL12]

1. Klik op **Voltooien**.

   ![De knop Voltooien][CL13]

IntelliJ importeert de Spring Boot-app als een project en de structuur wordt weergegeven wanneer het importeren is voltooid.

![Spring Boot-app in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Uw Spring opstart opbouwen app

### <a name="build-the-app-by-using-the-maven-pom"></a>De app bouwen met behulp van de POM Maven

1. Open het werkvenster Maven als deze nog niet is geopend. Klik op **weergave** > **Windows hulpprogramma** > **Maven-projecten**.

   ![Hulpprogramma voor Windows en Maven-projecten opdrachten][BU01]

1. In het venster Maven-hulpprogramma met de rechtermuisknop op **pakket** en selecteer **uitvoeren Maven Build**. (Als uw Maven-project niet automatisch weergegeven wordt, klikt u op de **opnieuw importeren** pictogram op de werkbalk Maven.)

   ![Build Maven-opdracht uitvoeren][BU02]

1. IntelliJ moet worden weergegeven in een **BUILD SUCCESS** wanneer uw app Spring Boot is gemaakt.

   ![BUILD SUCCESS bericht][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Maken van een artefact klaar voor implementatie

Voor het publiceren van uw app Spring opstart, moet u een artefact implementatie gereed te maken. Voer de volgende stappen uit:

1. Open IntelliJ uw web-app-project.

1. Klik op **bestand**, en klik vervolgens op **projectstructuur**.

   ![Opdracht voor project-structuur][ART01]

1. Klik op het groen plusteken (**+**) symbool een artefact toevoegen, klikt u op **JAR**, en klik vervolgens op **leeg**.

   ![Toevoegen van een artefact][ART02]

1. Naam van uw artefacten terwijl u ervoor dat u niet de extensie "JAR" toevoegen en geef vervolgens de doelmap voor de uitvoer Maven.

   ![Artefact-eigenschappen opgeven][ART03]

1. Maak een manifest voor uw artefacten (optioneel):

   a. Klik op **Manifest maken**.

      ![Klik op de knop maken Manifest][ART04a]

   b. Kies het standaardpad voor het artefact en klik vervolgens op **OK**.

      ![Artefacten pad opgeven][ART04b]

   c. Klik op het weglatingsteken (**...** ) de hoofdklasse vinden.

      ![Zoek hoofdklasse][ART04c]

   d. Kies uw hoofdklasse en klik vervolgens op **OK**.

      ![Belangrijkste klasse op te geven][ART04d]

1. Klik op **OK**.

   ![Sluit het dialoogvenster Project-structuur][ART05]

> [!NOTE]
> Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op de website JetBrains.
>

### <a name="build-the-artifact-for-deployment"></a>Maken van het artefact voor implementatie

1. Klik op **bouwen**, en klik vervolgens op **artefacten**.

   ![Artefacten opdracht bouwen][BU04]

1. Wanneer de **bouwen artefact** contextmenu weergegeven, klikt u op **bouwen**.

   ![Contextmenu artefact bouwen][BU05]

IntelliJ het voltooide artefact voor uw app Spring opstarten moet worden weergegeven in het venster van het hulpprogramma project.

   ![Gemaakte artefact][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Uw web-app publiceren naar Azure met behulp van Docker-container

1. Als u niet hebt aangemeld bij uw Azure-account, volg de stappen in [aanmelden instructies voor de Azure-Toolkit voor IntelliJ][Azure Sign In for IntelliJ].

1. In het venster van het hulpprogramma Projectverkenner met de rechtermuisknop op het project en selecteer vervolgens **Azure** > **publiceren als Docker-Container**.

   ![Als de opdracht Docker-Container publiceren][PU01]

1. Wanneer de **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven, worden alle bestaande Docker-hosts weergegeven. Als u kiest voor het implementeren van een bestaande host, kunt u doorgaan met stap 4. Gebruik anders de volgende stappen uit voor het maken van een host:

   a. Klik op het groen plusteken (**+**) symbool.

      ![Een nieuwe Docker-host toevoegen][PU02]

   b. Wanneer de **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u de standaardinstellingen accepteren of kunt u aangepaste instellingen voor uw nieuwe Docker-host. (Zie voor gedetailleerde beschrijvingen van de verschillende instellingen [een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u hebt opgegeven welke instellingen u wilt gebruiken.

      ![Geef opties voor Docker-host][PU03a]

   c. U kunt bestaande inloggegevens van een Azure sleutelkluis gebruiken of kunt u nieuwe Docker-aanmeldingsreferenties opgeven. Klik op **voltooien** wanneer u uw opties hebt opgegeven.

      ![Geef referenties op Docker-host][PU03b]

1. Selecteer de Docker-host en klik vervolgens op **volgende**.

   ![Selecteer de Docker-host te gebruiken][PU04]

1. Op de laatste pagina van de **Docker-Container in Azure implementeren** dialoogvenster geeft u de volgende opties:

   a. U kunt een aangepaste naam voor de container die als host voor uw Docker-container fungeert opgeven of u kunt de standaardwaarde accepteren.

   b. Geef de TCP-poorten voor uw docker-host met behulp van de volgende syntaxis: *[externe poort]*:*[interne poort]*. Bijvoorbeeld: **80:8080** Hiermee geeft u een externe poort 80 en de interne Spring opstarten standaardpoort 8080.
   
      Als u uw interne poort (bijvoorbeeld door het bewerken van het bestand application.yml) aangepast hebt, moet u het poortnummer opgeven voor de juiste routering uitgevoerd in Azure.

   c. Nadat u deze opties hebt geconfigureerd, klikt u op **voltooien**.

   ![Een Docker-container in Azure implementeren][PU05]

1. Wanneer de Toolkit Azure is gepubliceerd, de Azure Activity Log weergegeven **gepubliceerde** voor de status.

   ![Docker-host is geïmplementeerd][PU06]

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

Zie voor meer informatie over aanvullende methoden voor het maken van opstarten Spring apps met behulp van IntelliJ, [Spring Boot-projecten maken](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) op de website JetBrains.

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[artefacten configureren]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL01.png
[CL02a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02a.png
[CL02b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL02b.png
[CL03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL09.png
[CL10]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL10.png
[CL11]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL11.png
[CL12]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL12.png
[CL13]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL13.png
[CL14]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/CL14.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART03.png
[ART04a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04a.png
[ART04b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04b.png
[ART04c]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04c.png
[ART04d]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART04d.png
[ART05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/ART05.png

[BU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU02.png
[BU03]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU03.png
[BU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU04.png
[BU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU05.png
[BU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/BU06.png

[PU01]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU02.png
[PU03a]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03a.png
[PU03b]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU03b.png
[PU04]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-intellij-publish-spring-boot-docker-app/PU06.png
