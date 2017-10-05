---
title: Een .NET-app in een container implementeren in Azure Service Fabric | Microsoft Docs
description: "Leert u hoe u een .NET-app in Visual Studio in een Docker-Container van het pakket. Deze nieuwe 'container'-app wordt geïmplementeerd op een Service Fabric-cluster."
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
ms.openlocfilehash: 484db494e7975df950543d19bf841a4df7cdd139
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-to-azure-service-fabric"></a><span data-ttu-id="71139-104">Een .NET-toepassing in een Windows-container implementeren op Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="71139-104">Deploy a .NET application in a Windows container to Azure Service Fabric</span></span>

<span data-ttu-id="71139-105">Deze zelfstudie laat zien hoe u een bestaande ASP.NET-toepassing in een Windows-container in Azure implementeren.</span><span class="sxs-lookup"><span data-stu-id="71139-105">This tutorial shows you how to deploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="71139-106">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="71139-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="71139-107">Maak een Docker-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71139-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="71139-108">Een bestaande toepassing containerize</span><span class="sxs-lookup"><span data-stu-id="71139-108">Containerize an existing application</span></span>
> * <span data-ttu-id="71139-109">Continue integratie met Visual Studio en VSTS instellen</span><span class="sxs-lookup"><span data-stu-id="71139-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71139-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="71139-110">Prerequisites</span></span>

1. <span data-ttu-id="71139-111">Installeer [Docker CE voor Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) zodat u containers op Windows 10 uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="71139-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="71139-112">Vertrouwd raken met de [Windows 10 Containers Quick Start][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="71139-112">Familiarize yourself with the [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="71139-113">Download de [Fabrikam Fiber CallCenter] [ link-fabrikam-github] voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="71139-113">Download the [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="71139-114">Installeer [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="71139-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="71139-115">Installeer de [uitbreiding continue levering van hulpprogramma's voor Visual Studio 2017][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="71139-115">Install the [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="71139-116">Maak een [Azure-abonnement] [ link-azure-subscription] en een [Visual Studio Team Services-account][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="71139-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="71139-117">Een cluster maken in Azure</span><span class="sxs-lookup"><span data-stu-id="71139-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-the-application"></a><span data-ttu-id="71139-118">De toepassing containerize</span><span class="sxs-lookup"><span data-stu-id="71139-118">Containerize the application</span></span>

<span data-ttu-id="71139-119">Nu dat u hebt een [Service Fabric-cluster wordt uitgevoerd in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) bent u klaar voor een beperkte toepassing maken en implementeren.</span><span class="sxs-lookup"><span data-stu-id="71139-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready to create and deploy a containerized application.</span></span> <span data-ttu-id="71139-120">Voor het starten van onze toepassing wordt uitgevoerd in een container, moeten we voegen **Docker ondersteuning** aan het project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71139-120">To start running our application in a container, we need to add **Docker Support** to the project in Visual Studio.</span></span> <span data-ttu-id="71139-121">Bij het toevoegen van **Docker ondersteuning** aan de toepassing, twee dingen gebeuren.</span><span class="sxs-lookup"><span data-stu-id="71139-121">When you add **Docker support** to the application, two things happen.</span></span> <span data-ttu-id="71139-122">Eerst een _Dockerfile_ wordt toegevoegd aan het project.</span><span class="sxs-lookup"><span data-stu-id="71139-122">First, a _Dockerfile_ is added to the project.</span></span> <span data-ttu-id="71139-123">Dit nieuwe bestand wordt beschreven hoe de installatiekopie van de container kan worden opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="71139-123">This new file describes how the container image is to be built.</span></span> <span data-ttu-id="71139-124">Vervolgens tweede, een nieuwe _docker compose_ project wordt toegevoegd aan de oplossing.</span><span class="sxs-lookup"><span data-stu-id="71139-124">Then second, a new _docker-compose_ project is added to the solution.</span></span> <span data-ttu-id="71139-125">Het nieuwe project bevat enkele docker compose bestanden.</span><span class="sxs-lookup"><span data-stu-id="71139-125">The new project contains a few docker-compose files.</span></span> <span data-ttu-id="71139-126">Docker compose bestanden kunnen worden gebruikt om te beschrijven hoe de container wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71139-126">Docker-compose files can be used to describe how the container is run.</span></span>

<span data-ttu-id="71139-127">Meer informatie over het werken met [Container met Visual Studio Tools][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="71139-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="71139-128">Als dit de eerste keer dat u Windows-container installatiekopieën op uw computer uitvoert, moet de base afbeeldingen voor uw containers Docker CE halen.</span><span class="sxs-lookup"><span data-stu-id="71139-128">If it is the first time you are running Windows container images on your computer, Docker CE must pull down the base images for your containers.</span></span> <span data-ttu-id="71139-129">De afbeeldingen in deze zelfstudie gebruikt zijn 14 GB.</span><span class="sxs-lookup"><span data-stu-id="71139-129">The images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="71139-130">Opwekken en voer de volgende terminal opdracht voor het ophalen van de basisinstallatiekopieën:</span><span class="sxs-lookup"><span data-stu-id="71139-130">Go ahead and run the following terminal command to pull the base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="71139-131">Docker-ondersteuning toevoegen</span><span class="sxs-lookup"><span data-stu-id="71139-131">Add Docker support</span></span>

<span data-ttu-id="71139-132">Open de [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] bestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="71139-132">Open the [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="71139-133">Met de rechtermuisknop op de **FabrikamFiber.Web** project > **toevoegen** > **Docker ondersteuning**.</span><span class="sxs-lookup"><span data-stu-id="71139-133">Right-click the **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="71139-134">Ondersteuning voor SQL toevoegen</span><span class="sxs-lookup"><span data-stu-id="71139-134">Add support for SQL</span></span>

<span data-ttu-id="71139-135">Deze toepassing wordt SQL gebruikt als de gegevensprovider zodat een SQL-server vereist is voor het uitvoeren van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="71139-135">This application uses SQL as the data provider, so a SQL server is required to run the application.</span></span> <span data-ttu-id="71139-136">Verwijzen naar een installatiekopie van SQL Server-container in onze docker-compose.override.yml-bestand.</span><span class="sxs-lookup"><span data-stu-id="71139-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="71139-137">Open in Visual Studio **Solution Explorer**, vinden **docker compose**, en open het bestand **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="71139-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open the file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="71139-138">Navigeer naar de `services:` knooppunt toevoegen van een knooppunt met de naam `db:` waarmee wordt gedefinieerd met de SQL Server-vermelding voor de container.</span><span class="sxs-lookup"><span data-stu-id="71139-138">Navigate to the `services:` node, add a node named `db:` that defines the SQL Server entry for the container.</span></span>

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
><span data-ttu-id="71139-139">U kunt SQL-servers die u liever voor lokale foutopsporing gebruiken, zolang deze bereikbaar is vanaf de host is.</span><span class="sxs-lookup"><span data-stu-id="71139-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="71139-140">Echter, **localdb** biedt geen ondersteuning voor `container -> host` communicatie.</span><span class="sxs-lookup"><span data-stu-id="71139-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="71139-141">Met SQL Server in een container biedt geen ondersteuning voor vastleggen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="71139-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="71139-142">Wanneer de container wordt gestopt, worden uw gegevens worden gewist.</span><span class="sxs-lookup"><span data-stu-id="71139-142">When the container stops, your data is erased.</span></span> <span data-ttu-id="71139-143">Gebruik deze configuratie niet voor productie.</span><span class="sxs-lookup"><span data-stu-id="71139-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="71139-144">Navigeer naar de `fabrikamfiber.web:` knooppunt en het toevoegen van een onderliggend knooppunt met de naam `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="71139-144">Navigate to the `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="71139-145">Dit zorgt ervoor dat de `db` (de SQL Server-container)-service wordt gestart voordat onze webtoepassing (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="71139-145">This ensures that the `db` service (the SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-the-web-config"></a><span data-ttu-id="71139-146">Bijwerken van de webconfiguratie</span><span class="sxs-lookup"><span data-stu-id="71139-146">Update the web config</span></span>

<span data-ttu-id="71139-147">Terug in de **FabrikamFiber.Web** project, het bijwerken van de verbindingsreeks in de **web.config** bestand om te verwijzen naar de SQL-Server in de container.</span><span class="sxs-lookup"><span data-stu-id="71139-147">Back in the **FabrikamFiber.Web** project, update the connection string in the **web.config** file, to point to the SQL Server in the container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="71139-148">Als u wilt gebruiken een ander wordt SQL Server tijdens het bouwen van een release bouwen van uw webtoepassing, nog een verbindingsreeks toevoegen aan uw web.release.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="71139-148">If you want to use a different SQL Server when building a release build of your web application, add another connection string to your web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="71139-149">De container testen</span><span class="sxs-lookup"><span data-stu-id="71139-149">Test your container</span></span>

<span data-ttu-id="71139-150">Druk op **F5** uitvoeren en fouten opsporen in de toepassing in de container.</span><span class="sxs-lookup"><span data-stu-id="71139-150">Press **F5** to run and debug the application in your container.</span></span>

<span data-ttu-id="71139-151">Rand opent van uw toepassing gedefinieerde starten-pagina met het IP-adres van de container op het interne netwerk met NAT (meestal 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="71139-151">Edge opens your application's defined launch page using the IP address of the container on the internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="71139-152">Zie voor meer informatie over foutopsporing in toepassingen in containers met behulp van Visual Studio 2017, [in dit artikel][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="71139-152">To learn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![Voorbeeld van fabrikam in een container][image-web-preview]

<span data-ttu-id="71139-154">De container is nu klaar om te worden gebouwd en verpakt in een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="71139-154">The container is now ready to be built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="71139-155">Zodra u de installatiekopie van het container gebouwd op uw computer hebt, kunt u dit doorgeven aan een container-register en voeg alles naar beneden op elke host worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71139-155">Once you have the container image built on your machine, you can push it to any container registry and pull it down to any host to run.</span></span>

## <a name="get-the-application-ready-for-the-cloud"></a><span data-ttu-id="71139-156">Bereid u voor de toepassing voor de cloud</span><span class="sxs-lookup"><span data-stu-id="71139-156">Get the application ready for the cloud</span></span>

<span data-ttu-id="71139-157">Om de toepassing klaar is voor het uitvoeren in Service Fabric in Azure, moeten we twee stappen:</span><span class="sxs-lookup"><span data-stu-id="71139-157">To get the application ready for running in Service Fabric in Azure, we need to complete two steps:</span></span>

1. <span data-ttu-id="71139-158">De poort waarop we willen kunnen bereiken onze webtoepassing in de Service Fabric-cluster worden blootgesteld.</span><span class="sxs-lookup"><span data-stu-id="71139-158">Expose the port where we want to be able to reach our web application in the Service Fabric cluster.</span></span>
2. <span data-ttu-id="71139-159">Geef een productie gereed SQL-database voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="71139-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-the-port-for-the-app"></a><span data-ttu-id="71139-160">De poort voor de app weergeven</span><span class="sxs-lookup"><span data-stu-id="71139-160">Expose the port for the app</span></span>
<span data-ttu-id="71139-161">Het Service Fabric-cluster dat we hebben geconfigureerd, heeft poort *80* standaard geopend in de Azure Load Balancer, die een compromis tussen de binnenkomende verkeer naar het cluster.</span><span class="sxs-lookup"><span data-stu-id="71139-161">The Service Fabric cluster we have configured, has port *80* open by default in the Azure Load Balancer, that balances incoming traffic to the cluster.</span></span> <span data-ttu-id="71139-162">We kunnen onze container op deze poort beschikbaar via onze docker-compose.yml-bestand.</span><span class="sxs-lookup"><span data-stu-id="71139-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="71139-163">Open in Visual Studio **Solution Explorer**, vinden **docker compose**, en open het bestand **docker compose.override.yml**.</span><span class="sxs-lookup"><span data-stu-id="71139-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open the file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="71139-164">Wijzig de `fabrikamfiber.web:` knooppunt een onderliggend knooppunt met de naam toevoegen `ports:`.</span><span class="sxs-lookup"><span data-stu-id="71139-164">Modify the `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="71139-165">Een tekenreeks-vermelding toevoegen `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="71139-165">Add a string entry `- "80:80"`.</span></span>

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

### <a name="use-a-production-sql-database"></a><span data-ttu-id="71139-166">Gebruik een SQL-database voor productie</span><span class="sxs-lookup"><span data-stu-id="71139-166">Use a production SQL database</span></span>
<span data-ttu-id="71139-167">Wanneer in productie wordt uitgevoerd, moeten we onze gegevens behouden in de database.</span><span class="sxs-lookup"><span data-stu-id="71139-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="71139-168">Er is momenteel geen manier om te waarborgen permanente gegevens in een container, dus u productiegegevens niet opslaan in SQL Server in een container.</span><span class="sxs-lookup"><span data-stu-id="71139-168">There is currently no way to guarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="71139-169">U wordt aangeraden gebruikmaken van een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="71139-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="71139-170">Als u wilt instellen en uitvoeren van een beheerde SQL-Server in Azure, gaat u naar de [Azure SQL Database snelstartgidsen] [ link-azure-sql] artikel.</span><span class="sxs-lookup"><span data-stu-id="71139-170">To set up and run a managed SQL Server in Azure, visit the [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="71139-171">Houd er rekening mee te wijzigen van de verbindingsreeksen in de SQL-server in de **web.release.config** bestand de **FabrikamFiber.Web** project.</span><span class="sxs-lookup"><span data-stu-id="71139-171">Remember to change the connection strings to the SQL server in the **web.release.config** file in the **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="71139-172">Deze toepassing mislukt probleemloos als geen SQL-database bereikbaar is.</span><span class="sxs-lookup"><span data-stu-id="71139-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="71139-173">U kunt doorgaan en de toepassing implementeren met geen SQL-server.</span><span class="sxs-lookup"><span data-stu-id="71139-173">You can choose to go ahead and deploy the application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="71139-174">Met Visual Studio teamservices implementeren</span><span class="sxs-lookup"><span data-stu-id="71139-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="71139-175">Als u een implementatie met behulp van Visual Studio Team Services instelt, moet u voor het installeren van de [extensie continue levering van hulpprogramma's voor Visual Studio 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="71139-175">To set up deployment using Visual Studio Team Services, you need to install the [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="71139-176">Deze extensie kunt eenvoudig implementeren in Azure door Visual Studio Team Services configureren en ophalen van uw app geïmplementeerd voor uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="71139-176">This extension makes it easy to deploy to Azure by configuring Visual Studio Team Services and get your app deployed to your Service Fabric cluster.</span></span>

<span data-ttu-id="71139-177">Om te beginnen, moet uw code worden gehost in broncodebeheer.</span><span class="sxs-lookup"><span data-stu-id="71139-177">To get started, your code must be hosted in source control.</span></span> <span data-ttu-id="71139-178">De rest van deze sectie wordt ervan uitgegaan dat **git** wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="71139-178">The rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="71139-179">Een opslagplaats VSTS instellen</span><span class="sxs-lookup"><span data-stu-id="71139-179">Set up a VSTS repo</span></span>
<span data-ttu-id="71139-180">Klik op de rechterbenedenhoek van Visual Studio **toevoegen aan broncodebeheer** > **Git** (of welke optie u liever).</span><span class="sxs-lookup"><span data-stu-id="71139-180">At the bottom-right corner of Visual Studio, click **Add to Source Control** > **Git** (or whichever option you prefer).</span></span>

![Druk op de knop bron controle][image-source-control]

<span data-ttu-id="71139-182">In de _Team Explorer_ deelvenster, drukt u op **Git-opslagplaats publiceren**.</span><span class="sxs-lookup"><span data-stu-id="71139-182">In the _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="71139-183">Selecteer de naam van de opslagplaats VSTS en druk op **opslagplaats**.</span><span class="sxs-lookup"><span data-stu-id="71139-183">Select your VSTS repository name and press **Repository**.</span></span>

![opslagplaats naar VSTS publiceren][image-publish-repo]

<span data-ttu-id="71139-185">Nu dat uw code wordt gesynchroniseerd met een bron VSTS opslagplaats, kunt u continue integratie en continue levering kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="71139-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="71139-186">Continue levering instellen</span><span class="sxs-lookup"><span data-stu-id="71139-186">Setup continuous delivery</span></span>

<span data-ttu-id="71139-187">In _Solution Explorer_, met de rechtermuisknop op de **oplossing** > **continue levering configureren**.</span><span class="sxs-lookup"><span data-stu-id="71139-187">In _Solution Explorer_, right-click the **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="71139-188">Selecteer het Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="71139-188">Select the Azure Subscription.</span></span>

<span data-ttu-id="71139-189">Stel **Type Host** naar **Service Fabric-Cluster**.</span><span class="sxs-lookup"><span data-stu-id="71139-189">Set **Host Type** to **Service Fabric Cluster**.</span></span>

<span data-ttu-id="71139-190">Stel **doelhost** naar de service fabric-cluster die u in de vorige sectie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71139-190">Set **Target Host** to the service fabric cluster you created in the previous section.</span></span>

<span data-ttu-id="71139-191">Kies een **Container register** voor het publiceren van de container.</span><span class="sxs-lookup"><span data-stu-id="71139-191">Choose a **Container Registry** to publish your container to.</span></span>

>[!TIP]
><span data-ttu-id="71139-192">Gebruik de **bewerken** om te maken van een container-register.</span><span class="sxs-lookup"><span data-stu-id="71139-192">Use the **Edit** button to create a container registry.</span></span>

<span data-ttu-id="71139-193">Druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="71139-193">Press **OK**.</span></span>

![Setup service fabric continue integratie][image-setup-ci]
   
   <span data-ttu-id="71139-195">Zodra de configuratie is voltooid, wordt de container geïmplementeerd naar Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="71139-195">Once the configuration is completed, your container is deployed to Service Fabric.</span></span> <span data-ttu-id="71139-196">Wanneer u push-updates naar de opslagplaats voor een nieuwe build en versie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="71139-196">Whenever you push updates to the repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="71139-197">Het opbouwen van de container afbeeldingen nemen ongeveer 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="71139-197">Building the container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="71139-198">De eerste implementatie voor de Service Fabric-cluster zorgt ervoor dat de basis Windows Server Core-container afbeeldingen worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="71139-198">The first deployment to the Service Fabric cluster causes the base Windows Server Core container images to be downloaded.</span></span> <span data-ttu-id="71139-199">Het downloaden van de duurt aanvullende 5-10 minuten.</span><span class="sxs-lookup"><span data-stu-id="71139-199">The download takes additional 5-10 minutes to complete.</span></span>

<span data-ttu-id="71139-200">Blader naar de Fabrikam aanroep Center-toepassing met de url van het cluster: bijvoorbeeld *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="71139-200">Browse to the Fabrikam Call Center application using the url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="71139-201">Nu dat u hebt beperkte en de oplossing Fabrikam aanroep Center geïmplementeerd, kunt u opent de [Azure-portal] [ link-azure-portal] en de toepassing die wordt uitgevoerd in de Service Fabric zien.</span><span class="sxs-lookup"><span data-stu-id="71139-201">Now that you have containerized and deployed the Fabrikam Call Center solution, you can open the [Azure portal][link-azure-portal] and see the application running in Service Fabric.</span></span> <span data-ttu-id="71139-202">Probeer de toepassing, open een webbrowser en Ga naar de URL van uw Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="71139-202">To try the application, open a web browser and go to the URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71139-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="71139-203">Next steps</span></span>

<span data-ttu-id="71139-204">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="71139-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="71139-205">Maak een Docker-project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="71139-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="71139-206">Een bestaande toepassing containerize</span><span class="sxs-lookup"><span data-stu-id="71139-206">Containerize an existing application</span></span>
> * <span data-ttu-id="71139-207">Continue integratie met Visual Studio en VSTS instellen</span><span class="sxs-lookup"><span data-stu-id="71139-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance to the next tutorial to learn how to bind a custom SSL certificate to it.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate to Azure Web Apps](app-service-web-tutorial-custom-ssl.md)

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
