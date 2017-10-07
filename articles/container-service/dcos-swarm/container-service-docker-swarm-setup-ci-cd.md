---
title: aaaCI/CD met Azure Container Service- en Swarm | Microsoft Docs
description: Gebruik Azure Container Service met Docker Swarm, een Azure Container register- en Visual Studio Team Services toodeliver continu een toepassing met meerdere container .NET Core
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, Containers Micro-services, Swarm, Azure, Visual Studio teamservices, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a>Volledige CI/CD pijplijn toodeploy een toepassing met meerdere container in Azure Container Service met Docker Swarm met behulp van Visual Studio Team Services

Een van de Hallo grootste uitdagingen wanneer kunnen toodeliver moderne toepassingen ontwikkelt voor Hallo cloud wordt deze toepassingen continu. In dit artikel leert u meer informatie over het tooimplement een volledige continue integratie en implementatie (CI/CD)-pijplijn met Azure Container Service met Docker Swarm, het register van Azure-Container en Visual Studio Team Services bouwen en releasebeheer.

In dit artikel is gebaseerd op een eenvoudige toepassing beschikbaar is op [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), ontwikkelde met ASP.NET Core. Hallo-toepassing bestaat uit vier verschillende services: drie web-API's en een web-front-end:

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

Hallo-doel is toodeliver deze toepassingen continu in een Docker Swarm-cluster met behulp van Visual Studio Team Services. Hallo volgende afbeelding details van deze continue levering pijplijn:

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

Hier volgt een korte uitleg van Hallo stappen:

1. Codewijzigingen zijn doorgevoerd toohello source code opslagplaats (in dit geval GitHub) 
2. GitHub activeert een bouwen in Visual Studio Team Services 
3. Visual Studio Team Services Hallo meest recente versie van Hallo bronnen opgehaald en maakt alle Hallo installatiekopieën waaruit Hallo-toepassing 
4. Visual Studio Team Services pushes elke installatiekopie tooa Docker register gemaakt met behulp van hello Azure Container Registry-service 
5. Visual Studio Team Services activeert een nieuwe release 
6. Hallo release bepaalde opdrachten via SSH op master clusterknooppunt van hello Azure container service uitgevoerd 
7. Docker Swarm op Hallo cluster worden Hallo meest recente versie van het Hallo-installatiekopieën 
8. nieuwe versie van de toepassing hello Hallo wordt geïmplementeerd met behulp van Docker Compose 

## <a name="prerequisites"></a>Vereisten

Voordat u deze zelfstudie begint, moet u toocomplete Hallo taken te volgen:

- [Een Swarm-cluster in Azure Container Service maken](container-service-deployment.md)
- [Verbinding maken met de Hallo Swarm-cluster in Azure Container Service](../container-service-connect.md)
- [Een Azure container registry maken](../../container-registry/container-registry-get-started-portal.md)
- [Een Visual Studio Team Services-account en team project zijn gemaakt](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [Vertakken Hallo GitHub-opslagplaats tooyour GitHub-account](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

U moet ook een machine Ubuntu (14.04 of 16.04) met Docker geïnstalleerd. Deze computer wordt gebruikt door Visual Studio Team Services tijdens Hallo bouwen en de vrijgave van processen. Eenzijdige toocreate deze machine is beschikbaar in Hallo toouse Hallo-installatiekopie [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/). 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a>Stap 1: Uw Visual Studio Team Services-account configureren 

In deze sectie configureert u uw Visual Studio Team Services-account.

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a>Een Visual Studio Team Services Linux build-agent configureren

toocreate Docker-installatiekopieën en push die deze installatiekopieën naar een Azure container register van een Visual Studio Team Services bouwen, moet u tooregister een Linux-agent. U hebt deze installatieopties:

* [Een op Linux-agent implementeren](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [Docker toorun Hallo VSTS agent gebruiken](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a>Hallo Docker-integratie VSTS uitbreiding installeren

Microsoft biedt een uitbreiding toowork VSTS gebouwd met Docker en de vrijgave van processen. Deze uitbreiding is beschikbaar in Hallo [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker). Klik op **installeren** tooadd deze extensie tooyour VSTS account:

![Hallo Docker-integratie installeren](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

U kunt tooconnect tooyour VSTS rekening met uw referenties wordt gevraagd. 

### <a name="connect-visual-studio-team-services-and-github"></a>Verbinding maken met Visual Studio teamservices en GitHub

Een verbinding tussen uw project VSTS en uw GitHub-account instellen.

1. Klik in het project voor Visual Studio Team Services, op Hallo **instellingen** pictogram in het Hallo-werkbalk en selecteert u **Services**.

    ![Visual Studio teamservices - externe verbinding](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. Klik aan de linkerkant Hallo op **nieuwe Service-eindpunt** > **GitHub**.

    ![Visual Studio teamservices - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. tooauthorize VSTS toowork met uw GitHub-account, klikt u op **autoriseren** en volg de procedure Hallo in Hallo-venster dat wordt geopend.

    ![Visual Studio teamservices - autoriseren GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a>Verbinding maken met VSTS tooyour Azure container register en Azure Container Service-cluster

Hallo laatste stappen voordat u in Hallo CI/CD pipeline zijn tooconfigure externe verbindingen tooyour container register en uw Docker Swarm-cluster in Azure. 

1. In Hallo **Services** instellingen van uw project Visual Studio Team Services, Voeg een service-eindpunt van het type **Docker-register**. 

2. Voer in Hallo pop-upvenster dat wordt geopend, Hallo-URL en referenties op Hallo van uw Azure-container-register.

    ![Visual Studio teamservices - Docker-register](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. Voor Hallo Docker Swarm-cluster, voegt u een eindpunt van het type **SSH**. Voer vervolgens de gegevens van Hallo SSH-verbinding van uw Swarm-cluster.

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

Alle Hallo-configuratie wordt nu uitgevoerd. In de volgende stappen hello maakt u Hallo CI/CD pijplijn die is gebaseerd en Docker Swarm-cluster van Hallo toepassing toohello implementeert. 

## <a name="step-2-create-hello-build-definition"></a>Stap 2: Hallo build-definitie maken

In deze stap maakt u een build definitionfor instellen met uw project VSTS en Hallo build werkstroom definiëren voor de installatiekopieën van de container

### <a name="initial-definition-setup"></a>Initiële definitie setup

1. de definitie van een build toocreate tooyour Visual Studio Team Services project en klik op verbinding **bouwen & Release**. 

2. In Hallo **bouwen definities** sectie, klikt u op **+ nieuw**. Selecteer Hallo **leeg** sjabloon.

    ![Visual Studio teamservices - nieuwe bouwen definitie](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. Nieuwe build Hallo configureren met een GitHub-opslagplaats bron, selectievakje **continue integratie**, en selecteer Hallo agent wachtrij waar u uw Linux-agent is geregistreerd. Klik op **maken** toocreate Hallo bouwen definitie.

    ![Visual Studio teamservices - maken Build-definitie](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. Op Hallo **bouwen definities** pagina, opent u eerst Hallo **opslagplaats** tabblad en Hallo build toouse Hallo fork Hallo MyShop project dat u hebt gemaakt in Hallo vereisten configureren. Zorg ervoor dat u selecteert *acs docs* als Hallo **standaardvertakking**.

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. Op Hallo **Triggers** tabblad, Hallo build toobe geactiveerd na elke doorvoer configureren. Selecteer **continue integratie** en **Batch wijzigingen**.

    ![Visual Studio teamservices - configuratie van de Build-Trigger](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a>Hallo build werkstroom definiëren
de volgende stappen Hallo definiëren Hallo build werkstroom. Er zijn vijf container installatiekopieën toobuild voor Hallo *MyShop* toepassing. Elke installatiekopie gebouwd met behulp van Hallo die dockerfile zich in Hallo projectmappen bevinden:

* ProductsApi
* Proxy
* RatingsApi
* RecommandationsApi
* Winkelpagina

U moet tooadd twee Docker stappen voor elke installatiekopie, één toobuild Hallo afbeelding en één toopush Hallo image in hello Azure container register. 

1. tooadd een stap in Hallo build werkstroom, klikt u op **+ toevoegen build stap** en selecteer **Docker**.

    ![Visual Studio teamservices - toevoegen Build stappen](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. Voor elke installatiekopie, configureert u één stap die gebruikmaakt van Hallo `docker build` opdracht.

    ![Visual Studio teamservices - Docker bouwen](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    Bouwen voor Hallo bewerking, selecteert u het register Azure container hello **bouwen van een installatiekopie van een** actie en Hallo Dockerfile waarin elke installatiekopie. Set Hallo **Build context** als Hallo Dockerfile hoofdmap en definiëren Hallo **Installatiekopienaam**. 
    
    Zoals wordt weergegeven op de voorgaande scherm hello, start u Hallo installatiekopie met de naam met Hallo URI van de registratie van uw Azure-container. (U kunt ook een code build variabele tooparameterize Hallo van Hallo-installatiekopie, zoals Hallo build-id in dit voorbeeld gebruiken.)

3. Voor elke installatiekopie, configureert u een tweede stap die gebruikmaakt van Hallo `docker push` opdracht.

    ![Visual Studio teamservices - Docker-Push](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    Voor Hallo push-bewerking, selecteert u het register Azure container hello **een installatiekopie van een Push** actie, en Voer Hallo **Installatiekopienaam** die is ingebouwd in de vorige stap Hallo.

4. Nadat u hebt configureren Hallo build en stappen voor elk van de vijf installatiekopieën Hallo push, voeg dat meer uit twee stappen in Hallo bouwen werkstroom.

    a. Een opdrachtregeltaak die gebruikmaakt van een bash script tooreplace hello *BuildNumber* exemplaar in Hallo docker-compose.yml-bestand met de huidige Hallo bouwen id. Zie Hallo na scherm voor meer informatie.

    ![Visual Studio teamservices - Update opstellen bestand](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    b. Een taak die wordt neergezet Hallo bijgewerkt opstellen bestand als een artefact build zodat deze kan worden gebruikt in Hallo-versie. Zie Hallo na scherm voor meer informatie.

    ![Visual Studio Team Services - opstellen publiceren bestand](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. Klik op **opslaan** en de naam van de definitie van de build.

## <a name="step-3-create-hello-release-definition"></a>Stap 3: Hallo release-definitie maken

Visual Studio Team Services kunt u te[releases beheren in omgevingen](https://www.visualstudio.com/team-services/release-management/). U kunt continue implementatie toomake ervoor dat uw toepassing wordt geïmplementeerd op de verschillende omgevingen (zoals ontwikkelen, testen, preproductie en productie) in een goede manier inschakelen. U kunt een nieuwe omgeving met uw Azure Container Service Docker Swarm-cluster maken.

![Visual Studio teamservices - Release tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a>Installatie van de eerste release

1. toocreate de definitie van een release, klikt u op **Releases** > **+ Release**

2. tooconfigure hello artefact bron, klikt u op **artefacten** > **een artefact koppelingsbron**. Deze nieuwe versie definitie toohello build die u hebt gedefinieerd in de vorige stap Hallo hier een koppeling. Op deze manier is beschikbaar in Hallo release proces Hallo docker-compose.yml-bestand.

    ![Visual Studio teamservices - Release artefacten](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. tooconfigure hello release worden geactiveerd, klikt u op **Triggers** en selecteer **continue implementatie**. Set Hallo trigger op Hallo dezelfde artefact-bron. Deze instelling zorgt ervoor dat er een nieuwe release begint zodra Hallo build voltooid is.

    ![Visual Studio teamservices - Release-Triggers](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a>Hallo release werkstroom definiëren

Hallo release werkstroom bestaat uit twee taken die u toevoegt.

1. Configureren van een taak toosecurely kopie Hallo opstellen bestand tooa *implementeren* map op Hallo Docker Swarm-hoofdknooppunt, met behulp van Hallo SSH-verbinding u eerder hebt geconfigureerd. Zie Hallo na scherm voor meer informatie.

    ![Visual Studio teamservices - Release SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. Configureren van een tweede taak tooexecute een opdracht bash toorun `docker` en `docker-compose` opdrachten op Hallo hoofdknooppunt. Zie Hallo na scherm voor meer informatie.

    ![Visual Studio teamservices - Release Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    Hallo-opdracht is uitgevoerd op Hallo master gebruik Hallo Docker CLI en Hallo Docker Compose CLI toodo Hallo taken te volgen:

    - Aanmelding toohello Azure container register (hierbij drie build variab'les die zijn gedefinieerd in Hallo **variabelen** tabblad)
    - Hallo definiëren **DOCKER_HOST** variabele toowork met Hallo Swarm-eindpunt (: 2375)
    - Navigeer toohello *implementeren* map die is gemaakt door Hallo voorafgaand aan beveiligde kopieertaak en die Hallo docker-compose.yml-bestand bevat 
    - Uitvoeren van `docker-compose` opdrachten die pull-hallo nieuwe afbeeldingen, Hallo-services stoppen, verwijdert u Hallo services en Hallo containers te maken.

    >[!IMPORTANT]
    > Zoals wordt weergegeven op de voorgaande scherm hello, laat u Hallo **mislukken op STDERR** selectievakje uitgeschakeld. Dit is een belangrijk instelling, omdat `docker-compose` worden afgedrukt verschillende diagnostische berichten, zoals de containers zijn gestopt of op Hallo standaardfout uitvoer wordt verwijderd. Als u het selectievakje Hallo inschakelt, rapporteert Visual Studio Team Services dat fouten zijn opgetreden tijdens het Hallo-release, zelfs als alles goed gaat.
    >
3. Sla deze definitie voor de nieuwe versie.


>[!NOTE]
>Deze implementatie bevat enige uitvaltijd, omdat we Hallo oude services worden gestopt en Hallo nieuwe uitgevoerd. Het is mogelijk tooavoid dit als volgt een blauw-groen-implementatie.
>

## <a name="step-4-test-hello-cicd-pipeline"></a>Stap 4. Test Hallo CI/CD-pipeline

Nu u klaar bent met Hallo configuratie, is het tijd tootest dit nieuwe CI/CD-pijplijn. Hallo gemakkelijkste manier tootest tooupdate Hallo source code en doorvoeren Hallo is gewijzigd in uw GitHub-opslagplaats. Enkele seconden nadat u push-Hallo code, ziet u een nieuwe build uitgevoerd in Visual Studio Team Services. Zodra de installatie is voltooid, wordt een nieuwe release wordt geactiveerd en Hallo nieuwe versie van de toepassing hello op Hallo Azure Container Service-cluster implementeert.

## <a name="next-steps"></a>Volgende stappen

* Zie voor meer informatie over CI/CD met Visual Studio Team Services, Hallo [VSTS bouwen overzicht](https://www.visualstudio.com/docs/build/overview).
