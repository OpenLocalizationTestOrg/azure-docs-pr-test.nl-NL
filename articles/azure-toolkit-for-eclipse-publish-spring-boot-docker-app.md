---
title: aaaPublish een Spring Boot-app als een Docker-container met behulp van Azure Toolkit voor Eclipse Hallo | Microsoft Docs
description: Meer informatie over hoe toopublish een web-app tooMicrosoft Azure als een Docker-container met behulp van Azure Toolkit voor Eclipse Hallo.
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
ms.openlocfilehash: 29390c49c339a1ebb87cb3951b21cea01c0da15f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Een app Spring opstarten publiceren als een Docker-container met behulp van hello Azure Toolkit voor Eclipse

Hallo [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken. Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.

[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.

Deze zelfstudie wordt u begeleid Hallo stappen toodeploy een toepassing Spring opstarten als een Docker-container tooMicrosoft Azure via hello Azure Toolkit voor Eclipse.

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a>Hallo standaard Spring Boot Docker opslagplaats klonen

### <a name="import-hello-public-repository"></a>Importeren Hallo openbare opslagplaats

Hallo doorlopen volgende stappen Hallo Spring Boot Docker-opslagplaats tooyour lokale computer met behulp van IntelliJ klonen. Als u een opdrachtregel toouse wilt, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].

1. Open de Eclipse.

1. Klik op **bestand** > **importeren**.

   ![Menu van bestand importeren][CL01]

1. Wanneer Hallo **importeren** dialoogvenster wordt geopend:

   a. Vouw **Git**.

   b. Selecteer **projecten van Git**.
   
   c. Klik op **Volgende**.

   ![Dialoogvenster importeren][CL02]

1. Op Hallo **opslagplaats bron selecteren** pagina:

   a. Selecteer **URI klonen**.
   
   b. Klik op **Volgende**.

   ![Repository Source pagina selecteren][CL03]

1. Op Hallo **bron Git-opslagplaats** pagina:

   a. Voor **URI**, voer `https://github.com/spring-guides/gs-spring-boot-docker.git`. Deze stap moet automatisch invullen Hallo **Host** en **opslagplaats pad** velden Hello waarden corrigeren.
   
   b. Hallo Spring opstarten opslagplaats is openbaar, dus u moet geen tooenter uw Git-gebruikersnaam en wachtwoord.
   
   c. Klik op **Volgende**.

   ![Bronpagina Git-opslagplaats][CL04]

1. Op Hallo **vertakking selectie** pagina, klikt u op **volgende**.

   ![Selectie vertakkingpagina][CL05]

1. Op Hallo **lokale bestemming** pagina:

   a. Hallo lokale map waar u uw lokale opslagplaats wilt opgeven.
   
   b. Klik op **Volgende**.

   ![Lokale doelpagina][CL06]

1. Op Hallo **een toouse wizard voor het importeren van de projecten selecteren** pagina:

   a. Selecteer **importeren als een algemene project**.
   
   b. Klik op **Volgende**.

   ![Pagina 'Een toouse wizard voor het importeren van de projecten selecteren'][CL07]

1. Op Hallo **importeren projecten** pagina:

   a. Geef de projectnaam van uw.
   
   b. Klik op **Voltooien**.

   ![Pagina Projecten importeren][CL08]

1. Als het Hallo-opslagplaats met succes is gekloond, ziet u alle Hallo-bestanden die worden vermeld in Eclipse.

   ![Lokale-opslagplaats][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a>Maak een Maven-project vanuit uw lokale opslagplaats

Hallo Spring Boot Docker-opslagplaats bevat een voltooide Maven-project dat u voor deze zelfstudie gebruiken wilt. 

1. Klik op **bestand** > **importeren**.

   ![Opdracht in menu Hallo-bestand importeren][CL01]

1. Wanneer Hallo **importeren** dialoogvenster wordt geopend:

   a. Vouw **Maven**.
   
   b. Selecteer **bestaande Maven-projecten**.
   
   c. Klik op **Volgende**.

   ![Dialoogvenster importeren][MV01]

1. Op Hallo **Maven-projecten** pagina:

   a. Voor **hoofdmap**, geef Hallo **voltooid** map in uw lokale opslagplaats.
   
   b. Vouw Hallo **Geavanceerd** uit en voer de naam van een aangepaste voor **naam sjabloon**.
   
   c. Selecteer Hallo-vak voor Hallo **pom.xml** bestand in Hallo-project.
   
   d. Klik op **Voltooien**.

   ![Pagina maven-projecten][MV02]

1. Als Hallo Maven-project opent, ziet u een tweede die worden vermeld in Eclipse-project.

   ![Lokale Maven-project][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a>Uw app Spring opstarten maken met behulp van Maven

1. Selecteer in de Hallo Eclipse Projectverkenner, Hallo Maven-project.

1. Klik op **uitvoeren** > **uitvoeren als** > **Maven build**.

   ![Opdrachten toorun als Maven build][BU01]

1. Wanneer uw toepassing correct is samengesteld, bevat het consolevenster Hallo Hallo status.

   ![Geslaagde Maven build][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Uw web-app tooAzure publiceren met behulp van Docker-container

1. Selecteer in de Hallo Eclipse Projectverkenner, Hallo Maven-project.

1. Klik op Hallo Azure **publiceren** menu en klik vervolgens op **publiceren als Docker-Container**.

   ![Als de opdracht Docker-Container publiceren][PU01]

1. Wanneer Hallo **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven:

   a. Voer de naam van een aangepaste Docker-installatiekopie.
   
   b. Voor **artefact toodeploy**, geef Hallo pad toohello **gs-spring-boot-docker-0.1.0.jar** bestand dat u zojuist hebt gemaakt.

   ![Geef Docker-opties][PU02]

   Eventuele bestaande Docker-hosts worden weergegeven. 

1. Als u toodeploy tooan bestaande host kiest, kunt u toostep 5 overslaan. Gebruik anders Hallo stappen toocreate een host te volgen:

   a. Klik op **Add**.

      ![Een nieuwe Docker-host toevoegen][PU03]

   b. Wanneer Hallo **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u tooaccept Hallo standaardwaarden of kunt u aangepaste instellingen voor uw nieuwe Docker-host. (Zie voor gedetailleerde beschrijvingen van Hallo diverse instellingen [een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u welke instellingen toouse hebt opgegeven.

      ![Geef opties voor Docker-host][PU04]

   c. U kunt bestaande aanmeldingsreferenties toouse kiezen uit een Azure sleutelkluis, of u kunt tooenter nieuwe Docker-aanmeldingsreferenties. Klik op **voltooien** wanneer u uw opties hebt opgegeven.

      ![Geef referenties op Docker-host][PU05]

1. Selecteer de Docker-host en klik vervolgens op **volgende**.

   ![Selecteer Docker host toouse][PU06]

1. Op de laatste pagina Hallo Hallo **Docker-Container in Azure implementeren** dialoogvenster geeft u de Hallo volgende opties:

   a. U kunt toospecify een aangepaste naam voor het Hallo-container die als host voor uw Docker-container fungeert of kunt u de standaard Hallo accepteren.

   b. Voer Hallo TCP-poorten voor de docker-host met behulp van de volgende syntaxis Hallo: *[externe poort]*:*[interne poort]*. Bijvoorbeeld: **80:8080** geeft een externe poort 80 en Hallo interne Spring opstarten standaardpoort 8080.
   
      Als u uw interne poort (bijvoorbeeld door het bewerken van Hallo application.yml-bestand) aangepast hebt, moet u toospecify Hallo-poortnummer voor de juiste routering toooccur Hallo in Azure.

   c. Nadat u deze opties configureert, klikt u op **voltooien**.

   ![Een Docker-container in Azure implementeren][PU07]

1. Wanneer hello Azure Toolkit is gepubliceerd, geeft Azure Activity Log Hallo **gepubliceerde** voor Hallo status.

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
