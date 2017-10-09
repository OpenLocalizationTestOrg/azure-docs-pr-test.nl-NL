---
title: een app Spring opstarten als een Docker-container met behulp van aaaPublish hello Azure Toolkit voor IntelliJ | Microsoft Docs
description: Meer informatie over hoe toopublish een web-app tooMicrosoft Azure als een Docker-container met behulp van Azure Toolkit Hallo voor IntelliJ.
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
ms.openlocfilehash: 8964cb33fd8f61a39f091633ae9074d9658232fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Een app Spring opstarten publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ

Hallo [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.

[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.

Deze zelfstudie wordt u begeleid Hallo stappen toodeploy een toepassing Spring opstarten als een Docker-container tooMicrosoft Azure via hello Azure Toolkit voor IntelliJ.

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a>Hallo standaard Spring Boot Docker opslagplaats klonen

Hallo doorlopen volgende stappen Hallo Spring Boot Docker-opslagplaats met behulp van IntelliJ klonen. Als u een opdrachtregel toouse wilt, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].

1. Open IntelliJ.

1. Selecteer in het welkomstscherm Hallo Hallo **GitHub** optie in Hallo **uitchecken uit versiebeheer** lijst.

   ![GitHub-optie voor versiebeheer][CL01]

1. Geef uw referenties als u na vragen aan gebruiker toolog in.

   * Als u een gebruikersnaam en wachtwoord toolog in tooGitHub:

      ![In het dialoogvenster voor het invoeren van GitHub-gebruikersnaam en wachtwoord][CL02a]

   * Als u een token toolog in tooGitHub:

      ![In het dialoogvenster voor het invoeren van een GitHub-token][CL02b]

1. Voer **https://github.com/spring-guides/gs-spring-boot-docker.git** uw lokale pad en de mapinformatie opgeven voor de URL van de opslagplaats hello, en klik vervolgens op **kloon**.

   ![Dialoogvenster kloon-opslagplaats][CL03]

1. Wanneer u wordt gevraagd een IntelliJ-project, selecteer toocreate **Nee**.

   ![Een project IntelliJ toocreate weigeren][CL04]

1. Klik op de welkomstpagina Hallo **Project importeren**.

   ![Het project importeren][CL05]

1. Hallo-pad waar u Hallo Spring opstarten opslagplaats gekloond vinden, selecteer Hallo **voltooid** map onder de hoofdmap Hallo en klik vervolgens op **OK**.

   ![Selecteer een map voor importeren][CL06]

1. Wanneer u wordt gevraagd, selecteert u **project maken van bestaande bronnen**.

   ![Optie toocreate een project van bestaande bronnen][CL07]

1. Geef de projectnaam van uw of accepteer de standaardinstelling hello, Hallo pad toohello controleren **voltooid** map en klik vervolgens op **volgende**.

   ![Hallo projectnaam opgeven][CL08]

1. Alle mappen voor het importeren van aanpassen en klik vervolgens op **volgende**.

   ![Kies de mappen][CL09]

1. Hallo-bibliotheken tooimport bekijken en klik vervolgens op **volgende**.

   ![Bekijk de project-bibliotheken][CL10]

1. Hallo Modulestructuur bekijken en klik vervolgens op **volgende**.

   ![Bekijk de modulestructuur][CL11]

1. Geef uw JDK en klik vervolgens op **volgende**.

   ![Geef een JDK][CL12]

1. Klik op **Voltooien**.

   ![De knop Voltooien][CL13]

IntelliJ hello Spring opstarten app als een project importeert en Hallo structuur wordt weergegeven wanneer Hallo importeren is voltooid.

![Spring Boot-app in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a>Uw Spring opstart opbouwen app

### <a name="build-hello-app-by-using-hello-maven-pom"></a>Hallo-app maken met behulp van Maven POM Hallo

1. Hallo Maven hulpprogramma venster openen als deze nog niet is geopend. Klik op **weergave** > **Windows hulpprogramma** > **Maven-projecten**.

   ![Hulpprogramma voor Windows en Maven-projecten opdrachten][BU01]

1. Hallo Maven hulpprogramma venster met de rechtermuisknop op **pakket** en selecteer **uitvoeren Maven Build**. (Als uw Maven-project niet automatisch weergegeven wordt, klikt u op Hallo **opnieuw importeren** pictogram op Hallo Maven-werkbalk.)

   ![Build Maven-opdracht uitvoeren][BU02]

1. IntelliJ moet worden weergegeven in een **BUILD SUCCESS** wanneer uw app Spring Boot is gemaakt.

   ![BUILD SUCCESS bericht][BU03]

### <a name="create-a-deployment-ready-artifact"></a>Maken van een artefact klaar voor implementatie

toopublish uw app Spring opstart, moet u een implementatie-ready artefact toocreate. Gebruik Hallo stappen te volgen:

1. Open IntelliJ uw web-app-project.

1. Klik op **bestand**, en klik vervolgens op **projectstructuur**.

   ![Opdracht voor project-structuur][ART01]

1. Klik op Hallo groen plus (**+**) tooadd een artefact symbool, klikt u op **JAR**, en klik vervolgens op **leeg**.

   ![Toevoegen van een artefact][ART02]

1. Naam van uw artefacten bij om ervoor te zorgen niet tooadd extensie 'JAR' Hallo en geef vervolgens de doelmap Hallo op Hallo Maven uitvoer.

   ![Artefact-eigenschappen opgeven][ART03]

1. Maak een manifest voor uw artefacten (optioneel):

   a. Klik op **Manifest maken**.

      ![Klik op Hallo Manifest maken][ART04a]

   b. Kies Hallo standaardpad voor Hallo artefacten en klik vervolgens op **OK**.

      ![Artefacten pad opgeven][ART04b]

   c. Klik op Hallo weglatingsteken (**...** ) toolocate Hallo hoofdklasse.

      ![Zoek hoofdklasse][ART04c]

   d. Kies uw hoofdklasse en klik vervolgens op **OK**.

      ![Belangrijkste klasse op te geven][ART04d]

1. Klik op **OK**.

   ![Hallo structuur Project dialoogvenster te sluiten][ART05]

> [!NOTE]
> Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op Hallo JetBrains website.
>

### <a name="build-hello-artifact-for-deployment"></a>Hallo artefact voor implementatie maken

1. Klik op **bouwen**, en klik vervolgens op **artefacten**.

   ![Artefacten opdracht bouwen][BU04]

1. Wanneer Hallo **bouwen artefact** contextmenu weergegeven, klikt u op **bouwen**.

   ![Contextmenu artefact bouwen][BU05]

IntelliJ artefact Hallo voltooid voor uw app Spring opstarten moet worden weergegeven in venster Hallo project-hulpprogramma.

   ![Gemaakte artefact][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Uw web-app tooAzure publiceren met behulp van Docker-container

1. Als u tooyour Azure-account niet hebt aangemeld, stappen Hallo in [aanmelden instructies voor hello Azure Toolkit voor IntelliJ][Azure Sign In for IntelliJ].

1. Hallo Projectverkenner hulpprogramma-venster met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Azure** > **publiceren als Docker-Container**.

   ![Als de opdracht Docker-Container publiceren][PU01]

1. Wanneer Hallo **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven, worden alle bestaande Docker-hosts weergegeven. Als u toodeploy tooan bestaande host kiest, kunt u toostep 4 overslaan. Gebruik anders Hallo stappen toocreate een host te volgen:

   a. Klik op Hallo groen plus (**+**) symbool.

      ![Een nieuwe Docker-host toevoegen][PU02]

   b. Wanneer Hallo **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u tooaccept Hallo standaardwaarden of kunt u aangepaste instellingen voor uw nieuwe Docker-host. (Zie voor gedetailleerde beschrijvingen van Hallo diverse instellingen [een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u welke instellingen toouse hebt opgegeven.

      ![Geef opties voor Docker-host][PU03a]

   c. U kunt bestaande aanmeldingsreferenties toouse kiezen uit een Azure sleutelkluis, of u kunt tooenter nieuwe Docker-aanmeldingsreferenties. Klik op **voltooien** wanneer u uw opties hebt opgegeven.

      ![Geef referenties op Docker-host][PU03b]

1. Selecteer de Docker-host en klik vervolgens op **volgende**.

   ![Hallo Docker host toouse selecteren][PU04]

1. Op de laatste pagina Hallo Hallo **Docker-Container in Azure implementeren** dialoogvenster geeft u de Hallo volgende opties:

   a. U kunt toospecify een aangepaste naam voor het Hallo-container die als host voor uw Docker-container fungeert of kunt u de standaard Hallo accepteren.

   b. Voer Hallo TCP-poorten voor de docker-host met behulp van de volgende syntaxis Hallo: *[externe poort]*:*[interne poort]*. Bijvoorbeeld: **80:8080** geeft een externe poort 80 en Hallo interne Spring opstarten standaardpoort 8080.
   
      Als u uw interne poort (bijvoorbeeld door het bewerken van Hallo application.yml-bestand) aangepast hebt, moet u toospecify Hallo-poortnummer voor de juiste routering toooccur Hallo in Azure.

   c. Nadat u deze opties hebt geconfigureerd, klikt u op **voltooien**.

   ![Een Docker-container in Azure implementeren][PU05]

1. Wanneer hello Azure Toolkit is gepubliceerd, geeft Azure Activity Log Hallo **gepubliceerde** voor Hallo status.

   ![Docker-host is geïmplementeerd][PU06]

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

toolearn over aanvullende methoden voor het maken van opstarten Spring apps met behulp van IntelliJ, Zie [Spring Boot-projecten maken](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) op Hallo JetBrains website.

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
