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
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="8a2c3-104">Een .NET-toepassing in een Windows-container tooAzure Service Fabric implementeren</span><span class="sxs-lookup"><span data-stu-id="8a2c3-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="8a2c3-105">Deze zelfstudie leert u hoe toodeploy een bestaande ASP.NET-toepassing in een Windows-container in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="8a2c3-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="8a2c3-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a2c3-107">Maak een Docker-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a2c3-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="8a2c3-108">Een bestaande toepassing containerize</span><span class="sxs-lookup"><span data-stu-id="8a2c3-108">Containerize an existing application</span></span>
> * <span data-ttu-id="8a2c3-109">Continue integratie met Visual Studio en VSTS instellen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8a2c3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8a2c3-110">Prerequisites</span></span>

1. <span data-ttu-id="8a2c3-111">Installeer [Docker CE voor Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) zodat u containers op Windows 10 uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="8a2c3-112">Maak uzelf bekend met Hallo [Windows 10 Containers Quick Start][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="8a2c3-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="8a2c3-113">Hallo downloaden [Fabrikam Fiber CallCenter] [ link-fabrikam-github] voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="8a2c3-114">Installeer [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="8a2c3-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="8a2c3-115">Hallo installeren [extensie continue levering van hulpprogramma's voor Visual Studio 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="8a2c3-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="8a2c3-116">Maak een [Azure-abonnement] [ link-azure-subscription] en een [Visual Studio Team Services-account][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="8a2c3-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="8a2c3-117">Een cluster maken in Azure</span><span class="sxs-lookup"><span data-stu-id="8a2c3-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="8a2c3-118">De toepassing hello containerize</span><span class="sxs-lookup"><span data-stu-id="8a2c3-118">Containerize hello application</span></span>

<span data-ttu-id="8a2c3-119">Nu dat u hebt een [Service Fabric-cluster wordt uitgevoerd in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) u bent klaar toocreate en een beperkte toepassing implementeert.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="8a2c3-120">toostart onze toepassing wordt uitgevoerd in een container, moeten we tooadd **Docker ondersteuning** toohello-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="8a2c3-121">Bij het toevoegen van **Docker ondersteuning** toohello toepassing, twee dingen gebeuren.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="8a2c3-122">Eerst een _Dockerfile_ toohello project wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="8a2c3-123">Dit nieuwe bestand wordt beschreven waarom de installatiekopie van de container Hallo toobe gebouwd.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="8a2c3-124">Vervolgens tweede, een nieuwe _docker compose_ project toohello oplossing wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="8a2c3-125">Hallo nieuw project bevat enkele docker compose bestanden.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="8a2c3-126">Docker compose-bestanden kunnen worden gebruikt toodescribe hoe Hallo container wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="8a2c3-127">Meer informatie over het werken met [Container met Visual Studio Tools][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="8a2c3-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="8a2c3-128">Als het Hallo eerste keer dat u Windows-container installatiekopieën op uw computer uitvoert, moet Docker CE trek omlaag Hallo basisinstallatiekopieën voor uw containers.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="8a2c3-129">Hallo-afbeeldingen in deze zelfstudie gebruikt zijn 14 GB.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="8a2c3-130">Opwekken en Voer Hallo terminal opdracht toopull Hallo basisinstallatiekopieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="8a2c3-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="8a2c3-131">Docker-ondersteuning toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-131">Add Docker support</span></span>

<span data-ttu-id="8a2c3-132">Open Hallo [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] bestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="8a2c3-133">Klik met de rechtermuisknop Hallo **FabrikamFiber.Web** project > **toevoegen** > **Docker ondersteuning**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="8a2c3-134">Ondersteuning voor SQL toevoegen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-134">Add support for SQL</span></span>

<span data-ttu-id="8a2c3-135">Deze toepassing wordt SQL als gegevensprovider hello, zodat een SQL-server vereist toorun Hallo-toepassing is.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="8a2c3-136">Verwijzen naar een installatiekopie van SQL Server-container in onze docker-compose.override.yml-bestand.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="8a2c3-137">Open in Visual Studio **Solution Explorer**, vinden **docker compose**, en de bestandsnaam van de open Hallo **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="8a2c3-138">Navigeer toohello `services:` knooppunt toevoegen van een knooppunt met de naam `db:` Hallo SQL Server-vermelding voor de container hello te definiëren.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

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
><span data-ttu-id="8a2c3-139">U kunt SQL-servers die u liever voor lokale foutopsporing gebruiken, zolang deze bereikbaar is vanaf de host is.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="8a2c3-140">Echter, **localdb** biedt geen ondersteuning voor `container -> host` communicatie.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="8a2c3-141">Met SQL Server in een container biedt geen ondersteuning voor vastleggen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="8a2c3-142">Wanneer Hallo container wordt gestopt, worden uw gegevens worden gewist.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="8a2c3-143">Gebruik deze configuratie niet voor productie.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="8a2c3-144">Navigeer toohello `fabrikamfiber.web:` knooppunt en het toevoegen van een onderliggend knooppunt met de naam `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="8a2c3-145">Dit zorgt ervoor dat Hallo `db` (SQL Server-container Hallo)-service wordt gestart voordat onze webtoepassing (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="8a2c3-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="8a2c3-146">Hallo webconfiguratie bijwerken</span><span class="sxs-lookup"><span data-stu-id="8a2c3-146">Update hello web config</span></span>

<span data-ttu-id="8a2c3-147">Terug in Hallo **FabrikamFiber.Web** project, update Hallo-verbindingsreeks in Hallo **web.config** -bestand, toopoint toohello SQL-Server in het Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="8a2c3-148">Als u een andere SQL-Server tijdens het bouwen van een release bouwen van uw webtoepassing toouse wilt, kunt u een andere verbinding tekenreeks tooyour web.release.config-bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="8a2c3-149">De container testen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-149">Test your container</span></span>

<span data-ttu-id="8a2c3-150">Druk op **F5** toorun en foutopsporing Hallo-toepassing in de container.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="8a2c3-151">Rand opent van uw toepassing gedefinieerde starten-pagina met Hallo IP-adres van de container Hallo op Hallo interne NAT netwerk (meestal 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="8a2c3-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="8a2c3-152">Zie toolearn meer informatie over foutopsporing in toepassingen in containers met behulp van Visual Studio-2017 [in dit artikel][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="8a2c3-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![Voorbeeld van fabrikam in een container][image-web-preview]

<span data-ttu-id="8a2c3-154">Hallo-container is nu gereed toobe gebouwd en verpakt in een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="8a2c3-155">Zodra u de installatiekopie van de container Hallo gebouwd op uw computer hebt, kunt u dit tooany container register doorgeven en trek het omlaag tooany host toorun.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="8a2c3-156">De toepassing hello voorbereidingen voor Hallo cloud</span><span class="sxs-lookup"><span data-stu-id="8a2c3-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="8a2c3-157">tooget hello toepassing gereed is voor het uitvoeren in Service Fabric in Azure, moeten we toocomplete twee stappen:</span><span class="sxs-lookup"><span data-stu-id="8a2c3-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="8a2c3-158">Hallo-poort waar we toobe kunnen tooreach onze webtoepassing in Service Fabric-cluster hello wilt tonen.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="8a2c3-159">Geef een productie gereed SQL-database voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="8a2c3-160">Hallo-poort voor Hallo-app</span><span class="sxs-lookup"><span data-stu-id="8a2c3-160">Expose hello port for hello app</span></span>
<span data-ttu-id="8a2c3-161">Hallo Service Fabric-cluster we hebt geconfigureerd, is de poort *80* standaard geopend in hello Azure Load Balancer, die een compromis tussen de binnenkomende verkeer toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="8a2c3-162">We kunnen onze container op deze poort beschikbaar via onze docker-compose.yml-bestand.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="8a2c3-163">Open in Visual Studio **Solution Explorer**, vinden **docker compose**, en de bestandsnaam van de open Hallo **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="8a2c3-164">Hallo wijzigen `fabrikamfiber.web:` knooppunt een onderliggend knooppunt met de naam toevoegen `ports:`.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="8a2c3-165">Een tekenreeks-vermelding toevoegen `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-165">Add a string entry `- "80:80"`.</span></span>

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

### <a name="use-a-production-sql-database"></a><span data-ttu-id="8a2c3-166">Gebruik een SQL-database voor productie</span><span class="sxs-lookup"><span data-stu-id="8a2c3-166">Use a production SQL database</span></span>
<span data-ttu-id="8a2c3-167">Wanneer in productie wordt uitgevoerd, moeten we onze gegevens behouden in de database.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="8a2c3-168">Er zijn momenteel geen permanente manier tooguarantee-gegevens in een container, dus u productiegegevens niet opslaan in SQL Server in een container.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="8a2c3-169">U wordt aangeraden gebruikmaken van een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="8a2c3-170">tooset up en voer een beheerde SQL-Server in Azure, gaat u naar Hallo [Azure SQL Database snelstartgidsen] [ link-azure-sql] artikel.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="8a2c3-171">Houd er rekening mee toochange Hallo verbinding tekenreeksen toohello SQL-server in Hallo **web.release.config** bestand in Hallo **FabrikamFiber.Web** project.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="8a2c3-172">Deze toepassing mislukt probleemloos als geen SQL-database bereikbaar is.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="8a2c3-173">U kunt kiezen toogo vooruit en implementeer de toepassing hello met geen SQL-server.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="8a2c3-174">Met Visual Studio teamservices implementeren</span><span class="sxs-lookup"><span data-stu-id="8a2c3-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="8a2c3-175">tooset up implementatie met behulp van Visual Studio Team Services, moet u tooinstall hello [extensie continue levering van hulpprogramma's voor Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="8a2c3-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="8a2c3-176">Deze extensie maakt het eenvoudig toodeploy tooAzure door Visual Studio Team Services configureren en ophalen van uw app geïmplementeerd tooyour Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="8a2c3-177">tooget gestart, moet uw code worden gehost in broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="8a2c3-178">Hallo rest van deze sectie wordt ervan uitgegaan dat **git** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="8a2c3-179">Een opslagplaats VSTS instellen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-179">Set up a VSTS repo</span></span>
<span data-ttu-id="8a2c3-180">Hallo rechterbenedenhoek van Visual Studio, klikt u op **tooSource besturingselement toevoegen** > **Git** (of welke optie u liever).</span><span class="sxs-lookup"><span data-stu-id="8a2c3-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Druk op de knop Hallo bron][image-source-control]

<span data-ttu-id="8a2c3-182">In Hallo _Team Explorer_ deelvenster, drukt u op **Git-opslagplaats publiceren**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="8a2c3-183">Selecteer de naam van de opslagplaats VSTS en druk op **opslagplaats**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-183">Select your VSTS repository name and press **Repository**.</span></span>

![opslagplaats tooVSTS publiceren][image-publish-repo]

<span data-ttu-id="8a2c3-185">Nu dat uw code wordt gesynchroniseerd met een bron VSTS opslagplaats, kunt u continue integratie en continue levering kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="8a2c3-186">Continue levering instellen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-186">Setup continuous delivery</span></span>

<span data-ttu-id="8a2c3-187">In _Solution Explorer_, klik met de rechtermuisknop Hallo **oplossing** > **continue levering configureren**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="8a2c3-188">Selecteer hello Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="8a2c3-189">Stel **hosttype** te**Service Fabric-Cluster**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="8a2c3-190">Stel **doelhost** toohello service fabric-cluster die u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="8a2c3-191">Kies een **Container register** toopublish de container.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="8a2c3-192">Gebruik Hallo **bewerken** knop toocreate een container-register.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="8a2c3-193">Druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-193">Press **OK**.</span></span>

![Setup service fabric continue integratie][image-setup-ci]
   
   <span data-ttu-id="8a2c3-195">Zodra het Hallo-configuratie is voltooid, is de container geïmplementeerde tooService Fabric.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="8a2c3-196">Wanneer u updates toohello opslagplaats pushen wordt een nieuwe build en release uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8a2c3-197">Installatiekopieën van het gebouw Hallo container duren ongeveer 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="8a2c3-198">Hallo eerste implementatie toohello Service Fabric-cluster wordt Hallo base Windows Server Core-container installatiekopieën toobe gedownload.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="8a2c3-199">Hallo downloaden duurt toocomplete extra 5-10 minuten.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="8a2c3-200">Blader toohello Fabrikam aanroep Center-toepassing met behulp van de url van uw cluster Hallo: bijvoorbeeld *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="8a2c3-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="8a2c3-201">Nu dat u hebt beperkte en Hallo Fabrikam aanroep Center oplossing wordt geïmplementeerd, kunt u Hallo openen [Azure-portal] [ link-azure-portal] en het Hallo-toepassing uitgevoerd in de Service Fabric zien.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="8a2c3-202">tootry hello toepassing, open een webbrowser en ga toohello-URL van uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="8a2c3-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a2c3-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-203">Next steps</span></span>

<span data-ttu-id="8a2c3-204">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="8a2c3-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8a2c3-205">Maak een Docker-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8a2c3-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="8a2c3-206">Een bestaande toepassing containerize</span><span class="sxs-lookup"><span data-stu-id="8a2c3-206">Containerize an existing application</span></span>
> * <span data-ttu-id="8a2c3-207">Continue integratie met Visual Studio en VSTS instellen</span><span class="sxs-lookup"><span data-stu-id="8a2c3-207">Setup continuous integration with Visual Studio and VSTS</span></span>

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
