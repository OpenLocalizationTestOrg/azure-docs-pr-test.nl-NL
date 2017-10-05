---
title: Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor Eclipse | Microsoft Docs
description: Informatie over het publiceren van een web-app naar Microsoft Azure als een Docker-container met behulp van de Azure-Toolkit voor Eclipse.
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
ms.openlocfilehash: fcb60fcfbda26f5f37bfb0edcb01f8737188b6bc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a>Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor Eclipse

De [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een van de meer populaire projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.

[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.

Deze zelfstudie leert u de stappen voor het implementeren van een toepassing Spring opstarten als een Docker-container met Microsoft Azure met behulp van de Azure-Toolkit voor Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a>De standaard Spring Boot Docker-opslagplaats klonen

### <a name="import-the-public-repository"></a>De openbare opslagplaats importeren

De volgende stappen maakt u via de Spring Boot Docker-opslagplaats op uw lokale computer met behulp van IntelliJ klonen. Als u wilt een opdrachtregel te gebruiken, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].

1. Open de Eclipse.

1. Klik op **bestand** > **importeren**.

   ![Menu van bestand importeren][CL01]

1. Wanneer de **importeren** dialoogvenster wordt geopend:

   a. Vouw **Git**.

   b. Selecteer **projecten van Git**.
   
   c. Klik op **Volgende**.

   ![Dialoogvenster importeren][CL02]

1. Op de **opslagplaats bron selecteren** pagina:

   a. Selecteer **URI klonen**.
   
   b. Klik op **Volgende**.

   ![Repository Source pagina selecteren][CL03]

1. Op de **bron Git-opslagplaats** pagina:

   a. Voor **URI**, voer `https://github.com/spring-guides/gs-spring-boot-docker.git`. Deze stap moet automatisch invullen de **Host** en **opslagplaats pad** velden met de juiste waarden.
   
   b. De opslagplaats Spring Boot is openbaar, dus u hebt niet de Git-gebruikersnaam en wachtwoord invoeren.
   
   c. Klik op **Volgende**.

   ![Bronpagina Git-opslagplaats][CL04]

1. Op de **vertakking selectie** pagina, klikt u op **volgende**.

   ![Selectie vertakkingpagina][CL05]

1. Op de **lokale bestemming** pagina:

   a. Geef de lokale map waar u uw lokale opslagplaats.
   
   b. Klik op **Volgende**.

   ![Lokale doelpagina][CL06]

1. Op de **een wizard te gebruiken voor het importeren van de projecten selecteren** pagina:

   a. Selecteer **importeren als een algemene project**.
   
   b. Klik op **Volgende**.

   ![Pagina 'Een wizard te gebruiken voor het importeren van de projecten selecteren'][CL07]

1. Op de **importeren projecten** pagina:

   a. Geef de projectnaam van uw.
   
   b. Klik op **Voltooien**.

   ![Pagina Projecten importeren][CL08]

1. Als de opslagplaats met succes is gekloond, ziet u alle bestanden die worden vermeld in Eclipse.

   ![Lokale-opslagplaats][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Maak een Maven-project vanuit uw lokale opslagplaats

De versie die voorjaar Boot Docker-opslagplaats bevat een voltooide Maven-project dat u voor deze zelfstudie gebruiken wilt. 

1. Klik op **bestand** > **importeren**.

   ![De opdracht importeren in het menu bestand][CL01]

1. Wanneer de **importeren** dialoogvenster wordt geopend:

   a. Vouw **Maven**.
   
   b. Selecteer **bestaande Maven-projecten**.
   
   c. Klik op **Volgende**.

   ![Dialoogvenster importeren][MV01]

1. Op de **Maven-projecten** pagina:

   a. Voor **hoofdmap**, geef de **voltooid** map in uw lokale opslagplaats.
   
   b. Vouw de **Geavanceerd** uit en voer de naam van een aangepaste voor **naam sjabloon**.
   
   c. Selecteer het selectievakje uit voor de **pom.xml** bestand in het project.
   
   d. Klik op **Voltooien**.

   ![Pagina maven-projecten][MV02]

1. Als het Maven-project opent, ziet u een tweede die worden vermeld in Eclipse-project.

   ![Lokale Maven-project][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Uw app Spring opstarten maken met behulp van Maven

1. Selecteer het Maven-project in de Projectverkenner Eclipse.

1. Klik op **uitvoeren** > **uitvoeren als** > **Maven build**.

   ![Opdrachten uit te voeren als Maven bouwen][BU01]

1. Wanneer uw toepassing is is gebouwd, toont de status van het consolevenster.

   ![Geslaagde Maven build][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a>Uw web-app publiceren naar Azure met behulp van Docker-container

1. Selecteer het Maven-project in de Projectverkenner Eclipse.

1. Klik op de Azure **publiceren** menu en klik vervolgens op **publiceren als Docker-Container**.

   ![Als de opdracht Docker-Container publiceren][PU01]

1. Wanneer de **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven:

   a. Voer de naam van een aangepaste Docker-installatiekopie.
   
   b. Voor **artefact implementeren**, het pad opgeven naar de **gs-spring-boot-docker-0.1.0.jar** bestand dat u zojuist hebt gemaakt.

   ![Geef Docker-opties][PU02]

   Eventuele bestaande Docker-hosts worden weergegeven. 

1. Als u kiest voor het implementeren van een bestaande host, kunt u verder met stap 5. Gebruik anders de volgende stappen uit voor het maken van een host:

   a. Klik op **Add**.

      ![Een nieuwe Docker-host toevoegen][PU03]

   b. Wanneer de **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u de standaardinstellingen accepteren of kunt u aangepaste instellingen voor uw nieuwe Docker-host. (Zie voor gedetailleerde beschrijvingen van de verschillende instellingen [een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u hebt opgegeven welke instellingen u wilt gebruiken.

      ![Geef opties voor Docker-host][PU04]

   c. U kunt bestaande inloggegevens van een Azure sleutelkluis gebruiken of kunt u nieuwe Docker-aanmeldingsreferenties opgeven. Klik op **voltooien** wanneer u uw opties hebt opgegeven.

      ![Geef referenties op Docker-host][PU05]

1. Selecteer de Docker-host en klik vervolgens op **volgende**.

   ![Selecteer de Docker-host wilt laten gebruiken][PU06]

1. Op de laatste pagina van de **Docker-Container in Azure implementeren** dialoogvenster geeft u de volgende opties:

   a. U kunt een aangepaste naam voor de container die als host voor uw Docker-container fungeert opgeven of u kunt de standaardwaarde accepteren.

   b. Geef de TCP-poorten voor uw docker-host met behulp van de volgende syntaxis: *[externe poort]*:*[interne poort]*. Bijvoorbeeld: **80:8080** Hiermee geeft u een externe poort 80 en de interne Spring opstarten standaardpoort 8080.
   
      Als u uw interne poort (bijvoorbeeld door het bewerken van het bestand application.yml) aangepast hebt, moet u het poortnummer opgeven voor de juiste routering uitgevoerd in Azure.

   c. Nadat u deze opties configureert, klikt u op **voltooien**.

   ![Een Docker-container in Azure implementeren][PU07]

1. Wanneer de Toolkit Azure is gepubliceerd, de Azure Activity Log weergegeven **gepubliceerde** voor de status.

   ![Docker-host is geïmplementeerd][PU08]

## <a name="next-steps"></a>Volgende stappen

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
[Docker]: https://www.docker.com/
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[CL01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL01.png
[CL02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL02.png
[CL03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL03.png
[CL04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL04.png
[CL05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL05.png
[CL06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL06.png
[CL07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL07.png
[CL08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL08.png
[CL09]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/CL09.png

[MV01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV01.png
[MV02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV02.png
[MV03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/MV03.png

[BU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU01.png
[BU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/BU02.png

[PU01]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU01.png
[PU02]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU02.png
[PU03]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU03.png
[PU04]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU04.png
[PU05]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU05.png
[PU06]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU06.png
[PU07]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU07.png
[PU08]: ./media/azure-toolkit-for-eclipse-publish-spring-boot-docker-app/PU08.png
