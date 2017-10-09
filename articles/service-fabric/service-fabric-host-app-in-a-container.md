---
title: een .NET-app in een container tooAzure Service Fabric aaaDeploy | Microsoft Docs
description: "Leert u hoe toopackage een .NET-app in Visual Studio in een Docker-Container. Deze nieuwe 'container'-app wordt geïmplementeerd tooa Service Fabric-cluster."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Een .NET-toepassing in een Windows-container tooAzure Service Fabric implementeren

Deze zelfstudie leert u hoe toodeploy een bestaande ASP.NET-toepassing in een Windows-container in Azure.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Maak een Docker-project in Visual Studio
> * Een bestaande toepassing containerize
> * Continue integratie met Visual Studio en VSTS instellen

## <a name="prerequisites"></a>Vereisten

1. Installeer [Docker CE voor Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) zodat u containers op Windows 10 uitvoeren kunt.
2. Maak uzelf bekend met Hallo [Windows 10 Containers Quick Start][link-container-quickstart].
3. Hallo downloaden [Fabrikam Fiber CallCenter] [ link-fabrikam-github] voorbeeldtoepassing.
4. Installeer [Azure PowerShell][link-azure-powershell-install]
5. Hallo installeren [extensie continue levering van hulpprogramma's voor Visual Studio 2017][link-visualstudio-cd-extension]
6. Maak een [Azure-abonnement] [ link-azure-subscription] en een [Visual Studio Team Services-account][link-vsts-account]. 
7. [Een cluster maken in Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>De toepassing hello containerize

Nu dat u hebt een [Service Fabric-cluster wordt uitgevoerd in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) u bent klaar toocreate en een beperkte toepassing implementeert. toostart onze toepassing wordt uitgevoerd in een container, moeten we tooadd **Docker ondersteuning** toohello-project in Visual Studio. Bij het toevoegen van **Docker ondersteuning** toohello toepassing, twee dingen gebeuren. Eerst een _Dockerfile_ toohello project wordt toegevoegd. Dit nieuwe bestand wordt beschreven waarom de installatiekopie van de container Hallo toobe gebouwd. Vervolgens tweede, een nieuwe _docker compose_ project toohello oplossing wordt toegevoegd. Hallo nieuw project bevat enkele docker compose bestanden. Docker compose-bestanden kunnen worden gebruikt toodescribe hoe Hallo container wordt uitgevoerd.

Meer informatie over het werken met [Container met Visual Studio Tools][link-visualstudio-container-tools].

>[!NOTE]
>Als het Hallo eerste keer dat u Windows-container installatiekopieën op uw computer uitvoert, moet Docker CE trek omlaag Hallo basisinstallatiekopieën voor uw containers. Hallo-afbeeldingen in deze zelfstudie gebruikt zijn 14 GB. Opwekken en Voer Hallo terminal opdracht toopull Hallo basisinstallatiekopieën te volgen:
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Docker-ondersteuning toevoegen

Open Hallo [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] bestand in Visual Studio.

Klik met de rechtermuisknop Hallo **FabrikamFiber.Web** project > **toevoegen** > **Docker ondersteuning**.

### <a name="add-support-for-sql"></a>Ondersteuning voor SQL toevoegen

Deze toepassing wordt SQL als gegevensprovider hello, zodat een SQL-server vereist toorun Hallo-toepassing is. Verwijzen naar een installatiekopie van SQL Server-container in onze docker-compose.override.yml-bestand.

Open in Visual Studio **Solution Explorer**, vinden **docker compose**, en de bestandsnaam van de open Hallo **docker compose.override.yml**.

Navigeer toohello `services:` knooppunt toevoegen van een knooppunt met de naam `db:` Hallo SQL Server-vermelding voor de container hello te definiëren.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>U kunt SQL-servers die u liever voor lokale foutopsporing gebruiken, zolang deze bereikbaar is vanaf de host is. Echter, **localdb** biedt geen ondersteuning voor `container -> host` communicatie.

>[!WARNING]
>Met SQL Server in een container biedt geen ondersteuning voor vastleggen van gegevens. Wanneer Hallo container wordt gestopt, worden uw gegevens worden gewist. Gebruik deze configuratie niet voor productie.

Navigeer toohello `fabrikamfiber.web:` knooppunt en het toevoegen van een onderliggend knooppunt met de naam `depends_on:`. Dit zorgt ervoor dat Hallo `db` (SQL Server-container Hallo)-service wordt gestart voordat onze webtoepassing (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Hallo webconfiguratie bijwerken

Terug in Hallo **FabrikamFiber.Web** project, update Hallo-verbindingsreeks in Hallo **web.config** -bestand, toopoint toohello SQL-Server in het Hallo-container.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Als u een andere SQL-Server tijdens het bouwen van een release bouwen van uw webtoepassing toouse wilt, kunt u een andere verbinding tekenreeks tooyour web.release.config-bestand toevoegen.

### <a name="test-your-container"></a>De container testen

Druk op **F5** toorun en foutopsporing Hallo-toepassing in de container.

Rand opent van uw toepassing gedefinieerde starten-pagina met Hallo IP-adres van de container Hallo op Hallo interne NAT netwerk (meestal 172.x.x.x). Zie toolearn meer informatie over foutopsporing in toepassingen in containers met behulp van Visual Studio-2017 [in dit artikel][link-debug-container].

![Voorbeeld van fabrikam in een container][image-web-preview]

Hallo-container is nu gereed toobe gebouwd en verpakt in een Service Fabric-toepassing. Zodra u de installatiekopie van de container Hallo gebouwd op uw computer hebt, kunt u dit tooany container register doorgeven en trek het omlaag tooany host toorun.

## <a name="get-hello-application-ready-for-hello-cloud"></a>De toepassing hello voorbereidingen voor Hallo cloud

tooget hello toepassing gereed is voor het uitvoeren in Service Fabric in Azure, moeten we toocomplete twee stappen:

1. Hallo-poort waar we toobe kunnen tooreach onze webtoepassing in Service Fabric-cluster hello wilt tonen.
2. Geef een productie gereed SQL-database voor de toepassing.

### <a name="expose-hello-port-for-hello-app"></a>Hallo-poort voor Hallo-app
Hallo Service Fabric-cluster we hebt geconfigureerd, is de poort *80* standaard geopend in hello Azure Load Balancer, die een compromis tussen de binnenkomende verkeer toohello cluster. We kunnen onze container op deze poort beschikbaar via onze docker-compose.yml-bestand.

Open in Visual Studio **Solution Explorer**, vinden **docker compose**, en de bestandsnaam van de open Hallo **docker compose.override.yml**.

Hallo wijzigen `fabrikamfiber.web:` knooppunt een onderliggend knooppunt met de naam toevoegen `ports:`.

Een tekenreeks-vermelding toevoegen `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Gebruik een SQL-database voor productie
Wanneer in productie wordt uitgevoerd, moeten we onze gegevens behouden in de database. Er zijn momenteel geen permanente manier tooguarantee-gegevens in een container, dus u productiegegevens niet opslaan in SQL Server in een container.

U wordt aangeraden gebruikmaken van een Azure SQL Database. tooset up en voer een beheerde SQL-Server in Azure, gaat u naar Hallo [Azure SQL Database snelstartgidsen] [ link-azure-sql] artikel.

>[!NOTE]
>Houd er rekening mee toochange Hallo verbinding tekenreeksen toohello SQL-server in Hallo **web.release.config** bestand in Hallo **FabrikamFiber.Web** project.
>
>Deze toepassing mislukt probleemloos als geen SQL-database bereikbaar is. U kunt kiezen toogo vooruit en implementeer de toepassing hello met geen SQL-server.

## <a name="deploy-with-visual-studio-team-services"></a>Met Visual Studio teamservices implementeren

tooset up implementatie met behulp van Visual Studio Team Services, moet u tooinstall hello [extensie continue levering van hulpprogramma's voor Visual Studio 2017][link-visualstudio-cd-extension]. Deze extensie maakt het eenvoudig toodeploy tooAzure door Visual Studio Team Services configureren en ophalen van uw app geïmplementeerd tooyour Service Fabric-cluster.

tooget gestart, moet uw code worden gehost in broncodebeheer. Hallo rest van deze sectie wordt ervan uitgegaan dat **git** wordt gebruikt.

### <a name="set-up-a-vsts-repo"></a>Een opslagplaats VSTS instellen
Hallo rechterbenedenhoek van Visual Studio, klikt u op **tooSource besturingselement toevoegen** > **Git** (of welke optie u liever).

![Druk op de knop Hallo bron][image-source-control]

In Hallo _Team Explorer_ deelvenster, drukt u op **Git-opslagplaats publiceren**.

Selecteer de naam van de opslagplaats VSTS en druk op **opslagplaats**.

![opslagplaats tooVSTS publiceren][image-publish-repo]

Nu dat uw code wordt gesynchroniseerd met een bron VSTS opslagplaats, kunt u continue integratie en continue levering kunt configureren.

### <a name="setup-continuous-delivery"></a>Continue levering instellen

In _Solution Explorer_, klik met de rechtermuisknop Hallo **oplossing** > **continue levering configureren**.

Selecteer hello Azure-abonnement.

Stel **hosttype** te**Service Fabric-Cluster**.

Stel **doelhost** toohello service fabric-cluster die u hebt gemaakt in de vorige sectie Hallo.

Kies een **Container register** toopublish de container.

>[!TIP]
>Gebruik Hallo **bewerken** knop toocreate een container-register.

Druk op **OK**.

![Setup service fabric continue integratie][image-setup-ci]
   
   Zodra het Hallo-configuratie is voltooid, is de container geïmplementeerde tooService Fabric. Wanneer u updates toohello opslagplaats pushen wordt een nieuwe build en release uitgevoerd.
   
   >[!NOTE]
   >Installatiekopieën van het gebouw Hallo container duren ongeveer 15 minuten.
   >Hallo eerste implementatie toohello Service Fabric-cluster wordt Hallo base Windows Server Core-container installatiekopieën toobe gedownload. Hallo downloaden duurt toocomplete extra 5-10 minuten.

Blader toohello Fabrikam aanroep Center-toepassing met behulp van de url van uw cluster Hallo: bijvoorbeeld *http://mycluster.westeurope.cloudapp.azure.com*

Nu dat u hebt beperkte en Hallo Fabrikam aanroep Center oplossing wordt geïmplementeerd, kunt u Hallo openen [Azure-portal] [ link-azure-portal] en het Hallo-toepassing uitgevoerd in de Service Fabric zien. tootry hello toepassing, open een webbrowser en ga toohello-URL van uw Service Fabric-cluster.

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Maak een Docker-project in Visual Studio
> * Een bestaande toepassing containerize
> * Continue integratie met Visual Studio en VSTS instellen

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
