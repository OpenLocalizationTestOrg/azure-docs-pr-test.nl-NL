---
title: aaaCI/CD met Azure Container Service-Engine en Swarm-modus | Microsoft Docs
description: Azure Container Service-Engine gebruiken met Docker Swarm-modus, een Azure Container register- en Visual Studio Team Services toodeliver continu een toepassing met meerdere container .NET Core
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, Containers Micro-services, Swarm, Azure, Visual Studio Team Services, DevOps, ACS-Engine
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a>Volledige CI/CD pijplijn toodeploy een toepassing met meerdere container in Azure Container Service met de ACS-Engine en Docker Swarm-modus met behulp van Visual Studio Team Services

*In dit artikel is gebaseerd op [volledige CI/CD pipeline toodeploy een toepassing met meerdere container in Azure Container Service met Docker Swarm met behulp van Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentatie*

Tegenwoordig een van de Hallo grootste uitdagingen wanneer kunnen toodeliver moderne toepassingen ontwikkelt voor Hallo cloud wordt deze toepassingen continu. In dit artikel leert u hoe tooimplement een volledige continue integratie en implementatie (CI/CD) pipeline gebruiken: 
* Azure Container Service-Engine met Docker Swarm-modus
* Azure Container Registry
* Visual Studio Team Services

In dit artikel is gebaseerd op een eenvoudige toepassing beschikbaar is op [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), ontwikkelde met ASP.NET Core. Hallo-toepassing bestaat uit vier verschillende services: drie web-API's en een web-front-end:

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

Hallo-doel is toodeliver deze toepassingen continu in een modus voor Docker Swarm-cluster met behulp van Visual Studio Team Services. Hallo volgende afbeelding details van deze continue levering pijplijn:

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

Hier volgt een korte uitleg van Hallo stappen:

1. Codewijzigingen zijn doorgevoerd toohello source code opslagplaats (in dit geval GitHub) 
2. GitHub activeert een bouwen in Visual Studio Team Services 
3. Visual Studio Team Services Hallo meest recente versie van Hallo bronnen opgehaald en maakt alle Hallo installatiekopieën waaruit Hallo-toepassing 
4. Visual Studio Team Services pushes elke installatiekopie tooa Docker register gemaakt met behulp van hello Azure Container Registry-service 
5. Visual Studio Team Services activeert een nieuwe release 
6. Hallo release bepaalde opdrachten via SSH op master clusterknooppunt van hello Azure container service uitgevoerd 
7. Docker Swarm modus op Hallo cluster haalt Hallo meest recente versie van Hallo installatiekopieën 
8. nieuwe versie van de toepassing hello Hello wordt geïmplementeerd met behulp van Docker-Stack 

## <a name="prerequisites"></a>Vereisten

Voordat u deze zelfstudie begint, moet u toocomplete Hallo taken te volgen:

- [Een modus Swarm-cluster maken in Azure Container Service met de ACS-Engine](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [Verbinding maken met de Hallo Swarm-cluster in Azure Container Service](../container-service-connect.md)
- [Een Azure container registry maken](../../container-registry/container-registry-get-started-portal.md)
- [Een Visual Studio Team Services-account en team project zijn gemaakt](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Vertakken Hallo GitHub-opslagplaats tooyour GitHub-account](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> Hallo orchestrator Docker Swarm in Azure Container Service maakt gebruik van verouderde zelfstandige Swarm. Op dit moment Hallo geïntegreerd [Swarm modus](https://docs.docker.com/engine/swarm/) (in Docker 1.12 en hoger) is niet een ondersteunde orchestrator in Azure Container Service. Daarom gebruiken we [ACS-Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), community-bijgedragen [snelstartsjabloon](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), of een Docker-oplossing in Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com).
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Stap 1: Uw Visual Studio Team Services-account configureren 

In deze sectie configureert u uw Visual Studio Team Services-account. tooconfigure VSTS Services eindpunten in het project voor Visual Studio Team Services, klikt u op Hallo **instellingen** pictogram in het Hallo-werkbalk en selecteert u **Services**.

![Open Services-eindpunt](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a>Verbinding maken met Visual Studio Team Services en Azure-account

Een verbinding tussen uw project VSTS en uw Azure-account instellen.

1. Klik aan de linkerkant Hallo op **nieuwe Service-eindpunt** > **Azure Resource Manager**.
2. tooauthorize VSTS toowork met uw Azure-account, selecteer uw **abonnement** en klik op **OK**.

    ![Visual Studio teamservices - autoriseren van Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a>Verbinding maken met Visual Studio teamservices en GitHub

Een verbinding tussen uw project VSTS en uw GitHub-account instellen.

1. Klik aan de linkerkant Hallo op **nieuwe Service-eindpunt** > **GitHub**.
2. tooauthorize VSTS toowork met uw GitHub-account, klikt u op **autoriseren** en volg de procedure Hallo in Hallo-venster dat wordt geopend.

    ![Visual Studio teamservices - autoriseren GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a>Verbinding maken met VSTS tooyour Azure Container Service-cluster

Hallo laatste stappen voordat u in Hallo CI/CD pipeline zijn tooconfigure externe verbindingen tooyour Docker Swarm-cluster in Azure. 

1. Voor Hallo Docker Swarm-cluster, voegt u een eindpunt van het type **SSH**. Voer vervolgens de gegevens van Hallo SSH-verbinding van uw Swarm-cluster (master knooppunt).

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

Alle Hallo-configuratie wordt nu uitgevoerd. In de volgende stappen hello maakt u Hallo CI/CD pijplijn die is gebaseerd en Docker Swarm-cluster van Hallo toepassing toohello implementeert. 

## <a name="step-2-create-hello-build-definition"></a>Stap 2: Hallo build-definitie maken

In deze stap maakt u een definitie van de build instellen voor uw project VSTS en Hallo build werkstroom definiëren voor de installatiekopieën van de container

### <a name="initial-definition-setup"></a>Initiële definitie setup

1. de definitie van een build toocreate tooyour Visual Studio Team Services project en klik op verbinding **bouwen & Release**. In Hallo **bouwen definities** sectie, klikt u op **+ nieuw**. 

    ![Visual Studio teamservices - nieuwe bouwen definitie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. Selecteer Hallo **leeg proces**.

    ![Visual Studio teamservices - nieuwe, lege bouwen definitie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. Klik vervolgens op Hallo **variabelen** tabblad en twee nieuwe variabelen maken: **RegistryURL** en **AgentURL**. Hallo-waarden van het register en het Cluster Agents DNS plakken.

    ![Visual Studio teamservices - variabelen Buildconfiguratie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. Op Hallo **bouwen definities** pagina, open Hallo **Triggers** tabblad en Hallo build toouse continue integratie met Hallo fork Hallo MyShop project dat u hebt gemaakt in Hallo vereisten configureren. Selecteer **Batch wijzigingen**. Zorg ervoor dat u selecteert *docker-linux* als Hallo **vertakking specificatie**.

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. Tot slot op Hallo **opties** tabblad en wachtrij Hallo-agent te configureren**gehost Linux Preview**.

    ![Visual Studio teamservices - Agent de hostconfiguratie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a>Hallo build werkstroom definiëren
de volgende stappen Hallo definiëren Hallo build werkstroom. U moet eerst tooconfigure Hallo bron van Hallo-code. toodo deze Selecteer **GitHub** en uw **opslagplaats** en **vertakking** (docker-linux).

![Visual Studio teamservices - configureren broncode](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

Er zijn vijf container installatiekopieën toobuild voor Hallo *MyShop* toepassing. Elke installatiekopie gebouwd met behulp van Hallo die dockerfile zich in Hallo projectmappen bevinden:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* Winkelpagina

U moet twee Docker-stappen voor elke installatiekopie, één toobuild Hallo afbeelding en één toopush Hallo image in hello Azure container register. 

1. tooadd een stap in Hallo build werkstroom, klikt u op **+ toevoegen build stap** en selecteer **Docker**.

    ![Visual Studio teamservices - toevoegen Build stappen](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. Voor elke installatiekopie, configureert u één stap die gebruikmaakt van Hallo `docker build` opdracht.

    ![Visual Studio teamservices - Docker bouwen](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    Bouwen voor Hallo bewerking, selecteert u het register van de Container Azure hello **bouwen van een installatiekopie van een** actie en Hallo Dockerfile waarin elke installatiekopie. Set Hallo **werkmap** als hoofdmap Hallo Dockerfile, definieert u Hallo **Installatiekopienaam**, en selecteer **meest recente code bevatten**.
    
    Hallo Installatiekopienaam toobe is in deze indeling: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```. Vervang **[NAME]** met de naam van de installatiekopie Hallo:
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. Voor elke installatiekopie, configureert u een tweede stap die gebruikmaakt van Hallo `docker push` opdracht.

    ![Visual Studio teamservices - Docker-Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    Voor Hallo push-bewerking, selecteert u het register Azure container hello **een installatiekopie van een Push** actie, Voer Hallo **installatiekopie met de naam** die is ingebouwd in de vorige stap Hallo en selecteer **meest recente code opnemen** .

4. Nadat u hebt configureren Hallo build en stappen voor elk van de vijf installatiekopieën Hallo push, drie meer stappen in Hallo bouwen werkstroom toevoegen.

   ![Visual Studio teamservices - toevoegen opdrachtregelprogramma taak](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. Een opdrachtregeltaak die gebruikmaakt van een bash script tooreplace hello *RegistryURL* exemplaar in Hallo docker-compose.yml-bestand met Hallo RegistryURL variabele. 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio teamservices - Update opstellen-bestand met de Register-URL](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. Een opdrachtregeltaak die gebruikmaakt van een bash script tooreplace hello *AgentURL* exemplaar in Hallo docker-compose.yml-bestand met Hallo AgentURL variabele.
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. Een taak die wordt neergezet Hallo bijgewerkt opstellen bestand als een artefact build zodat deze kan worden gebruikt in Hallo-versie. Zie Hallo na scherm voor meer informatie.

         ![Visual Studio teamservices - publiceren artefacten](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - opstellen publiceren bestand](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. Klik op **opslaan en wachtrij** tootest de definitie van de build.

   ![Visual Studio teamservices - opslaan en wachtrij](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio teamservices - nieuwe wachtrij](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. Als hello **bouwen** juist is, hebt u toosee dit scherm:

  ![Visual Studio teamservices - Build is voltooid](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a>Stap 3: Hallo release-definitie maken

Visual Studio Team Services kunt u te[releases beheren in omgevingen](https://www.visualstudio.com/team-services/release-management/). U kunt continue implementatie toomake ervoor dat uw toepassing wordt geïmplementeerd op de verschillende omgevingen (zoals ontwikkelen, testen, preproductie en productie) in een goede manier inschakelen. U kunt een omgeving met uw Azure Container Service Docker Swarm modus cluster maken.

![Visual Studio teamservices - Release tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Installatie van de eerste release

1. toocreate de definitie van een release, klikt u op **Releases** > **+ Release**

2. tooconfigure hello artefact bron, klikt u op **artefacten** > **een artefact koppelingsbron**. Deze nieuwe versie definitie toohello build die u hebt gedefinieerd in de vorige stap Hallo hier een koppeling. Hallo docker-compose.yml-bestand is hierna is beschikbaar in Hallo release proces.

    ![Visual Studio teamservices - Release artefacten](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. tooconfigure hello release worden geactiveerd, klikt u op **Triggers** en selecteer **continue implementatie**. Set Hallo trigger op Hallo dezelfde artefact-bron. Deze instelling zorgt ervoor dat er een nieuwe release wordt gestart wanneer Hallo build voltooid is.

    ![Visual Studio teamservices - Release-Triggers](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. tooconfigure hello release variabelen, klikt u op **variabelen** en selecteer **+ variabele** toocreate drie nieuwe variabelen met Hallo-info van Hallo register: **docker.username**, **docker.password**, en **docker.registry**. Hallo-waarden van het register en het Cluster Agents DNS plakken.

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > Zoals u in het vorige scherm hello, klikt u op Hallo **vergrendeling** checkbox in docker.password. Deze instelling is belangrijk toorestrict Hallo wachtwoord.
    >

### <a name="define-hello-release-workflow"></a>Hallo release werkstroom definiëren

Hallo release werkstroom bestaat uit twee taken die u toevoegt.

1. Configureren van een taak toosecurely kopie Hallo opstellen bestand tooa *implementeren* map op Hallo Docker Swarm-hoofdknooppunt, met behulp van Hallo SSH-verbinding u eerder hebt geconfigureerd. Zie Hallo na scherm voor meer informatie.
    
    Bronmap:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```

    ![Visual Studio teamservices - Release SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. Configureren van een tweede taak tooexecute een opdracht bash toorun `docker` en `docker stack deploy` opdrachten op Hallo hoofdknooppunt. Zie Hallo na scherm voor meer informatie.

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio teamservices - Release Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    Hallo-opdracht uitgevoerd op Hallo master gebruikt Hallo Docker CLI en Hallo Docker Compose CLI toodo Hallo taken te volgen:

    - Meld u bij toohello Azure container register (hierbij drie build-variabelen die zijn gedefinieerd in Hallo **variabelen** tabblad)
    - Hallo definiëren **DOCKER_HOST** variabele toowork met Hallo Swarm-eindpunt (: 2375)
    - Navigeer toohello *implementeren* map die is gemaakt door Hallo voorafgaand aan beveiligde kopieertaak en die Hallo docker-compose.yml-bestand bevat 
    - Uitvoeren van `docker stack deploy` opdrachten die pull-hallo nieuwe afbeeldingen en Hallo containers te maken.

    >[!IMPORTANT]
    > Zoals u in het vorige scherm hello, laat u Hallo **mislukken op STDERR** selectievakje uitgeschakeld. Deze instelling kunt ons toocomplete Hallo release proces vanwege te`docker-compose` worden afgedrukt verschillende diagnostische berichten, zoals de containers zijn gestopt of op Hallo standaardfout uitvoer wordt verwijderd. Als u het selectievakje Hallo inschakelt, rapporteert Visual Studio Team Services dat fouten zijn opgetreden tijdens het Hallo-release, zelfs als alles goed gaat.
    >
3. Sla deze definitie voor de nieuwe versie.

## <a name="step-4-test-hello-cicd-pipeline"></a>Stap 4: Testen Hallo CI/CD-pipeline

Nu u klaar bent met Hallo configuratie, is het tijd tootest dit nieuwe CI/CD-pijplijn. Hallo gemakkelijkste manier tootest tooupdate Hallo source code en doorvoeren Hallo is gewijzigd in uw GitHub-opslagplaats. Enkele seconden nadat u push-Hallo code, ziet u een nieuwe build uitgevoerd in Visual Studio Team Services. Zodra de installatie is voltooid, wordt een nieuwe release wordt geactiveerd en Hallo nieuwe versie van de toepassing hello op Hallo Azure Container Service-cluster wordt geïmplementeerd.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over CI/CD met Visual Studio Team Services, Hallo [VSTS bouwen overzicht](https://www.visualstudio.com/docs/build/overview).
* Zie voor meer informatie over de ACS-Engine Hallo [ACS-Engine GitHub-repo-](https://github.com/Azure/acs-engine).
* Zie voor meer informatie over Docker Swarm modus Hallo [Docker Swarm modus overzicht](https://docs.docker.com/engine/swarm/).
