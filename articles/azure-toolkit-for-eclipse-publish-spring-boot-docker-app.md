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
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="82081-103">Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="82081-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="82081-104">De [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="82081-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="82081-105">Een van de meer populaire projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="82081-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="82081-106">[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.</span><span class="sxs-lookup"><span data-stu-id="82081-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="82081-107">Deze zelfstudie leert u de stappen voor het implementeren van een toepassing Spring opstarten als een Docker-container met Microsoft Azure met behulp van de Azure-Toolkit voor Eclipse.</span><span class="sxs-lookup"><span data-stu-id="82081-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repository"></a><span data-ttu-id="82081-108">De standaard Spring Boot Docker-opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="82081-108">Clone the default Spring Boot Docker repository</span></span>

### <a name="import-the-public-repository"></a><span data-ttu-id="82081-109">De openbare opslagplaats importeren</span><span class="sxs-lookup"><span data-stu-id="82081-109">Import the public repository</span></span>

<span data-ttu-id="82081-110">De volgende stappen maakt u via de Spring Boot Docker-opslagplaats op uw lokale computer met behulp van IntelliJ klonen.</span><span class="sxs-lookup"><span data-stu-id="82081-110">The following steps walk you through cloning the Spring Boot Docker repository to your local computer by using IntelliJ.</span></span> <span data-ttu-id="82081-111">Als u wilt een opdrachtregel te gebruiken, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="82081-111">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="82081-112">Open de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="82081-112">Open Eclipse.</span></span>

1. <span data-ttu-id="82081-113">Klik op **bestand** > **importeren**.</span><span class="sxs-lookup"><span data-stu-id="82081-113">Click **File** > **Import**.</span></span>

   ![Menu van bestand importeren][CL01]

1. <span data-ttu-id="82081-115">Wanneer de **importeren** dialoogvenster wordt geopend:</span><span class="sxs-lookup"><span data-stu-id="82081-115">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="82081-116">a.</span><span class="sxs-lookup"><span data-stu-id="82081-116">a.</span></span> <span data-ttu-id="82081-117">Vouw **Git**.</span><span class="sxs-lookup"><span data-stu-id="82081-117">Expand **Git**.</span></span>

   <span data-ttu-id="82081-118">b.</span><span class="sxs-lookup"><span data-stu-id="82081-118">b.</span></span> <span data-ttu-id="82081-119">Selecteer **projecten van Git**.</span><span class="sxs-lookup"><span data-stu-id="82081-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="82081-120">c.</span><span class="sxs-lookup"><span data-stu-id="82081-120">c.</span></span> <span data-ttu-id="82081-121">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-121">Click **Next**.</span></span>

   ![Dialoogvenster importeren][CL02]

1. <span data-ttu-id="82081-123">Op de **opslagplaats bron selecteren** pagina:</span><span class="sxs-lookup"><span data-stu-id="82081-123">On the **Select Repository Source** page:</span></span>

   <span data-ttu-id="82081-124">a.</span><span class="sxs-lookup"><span data-stu-id="82081-124">a.</span></span> <span data-ttu-id="82081-125">Selecteer **URI klonen**.</span><span class="sxs-lookup"><span data-stu-id="82081-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="82081-126">b.</span><span class="sxs-lookup"><span data-stu-id="82081-126">b.</span></span> <span data-ttu-id="82081-127">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-127">Click **Next**.</span></span>

   ![Repository Source pagina selecteren][CL03]

1. <span data-ttu-id="82081-129">Op de **bron Git-opslagplaats** pagina:</span><span class="sxs-lookup"><span data-stu-id="82081-129">On the **Source Git Repository** page:</span></span>

   <span data-ttu-id="82081-130">a.</span><span class="sxs-lookup"><span data-stu-id="82081-130">a.</span></span> <span data-ttu-id="82081-131">Voor **URI**, voer `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="82081-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="82081-132">Deze stap moet automatisch invullen de **Host** en **opslagplaats pad** velden met de juiste waarden.</span><span class="sxs-lookup"><span data-stu-id="82081-132">This step should automatically populate the **Host** and **Repository path** fields with the correct values.</span></span>
   
   <span data-ttu-id="82081-133">b.</span><span class="sxs-lookup"><span data-stu-id="82081-133">b.</span></span> <span data-ttu-id="82081-134">De opslagplaats Spring Boot is openbaar, dus u hebt niet de Git-gebruikersnaam en wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="82081-134">The Spring Boot repository is public, so you should not have to enter your Git username and password.</span></span>
   
   <span data-ttu-id="82081-135">c.</span><span class="sxs-lookup"><span data-stu-id="82081-135">c.</span></span> <span data-ttu-id="82081-136">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-136">Click **Next**.</span></span>

   ![Bronpagina Git-opslagplaats][CL04]

1. <span data-ttu-id="82081-138">Op de **vertakking selectie** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-138">On the **Branch Selection** page, click **Next**.</span></span>

   ![Selectie vertakkingpagina][CL05]

1. <span data-ttu-id="82081-140">Op de **lokale bestemming** pagina:</span><span class="sxs-lookup"><span data-stu-id="82081-140">On the **Local Destination** page:</span></span>

   <span data-ttu-id="82081-141">a.</span><span class="sxs-lookup"><span data-stu-id="82081-141">a.</span></span> <span data-ttu-id="82081-142">Geef de lokale map waar u uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82081-142">Specify the local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="82081-143">b.</span><span class="sxs-lookup"><span data-stu-id="82081-143">b.</span></span> <span data-ttu-id="82081-144">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-144">Click **Next**.</span></span>

   ![Lokale doelpagina][CL06]

1. <span data-ttu-id="82081-146">Op de **een wizard te gebruiken voor het importeren van de projecten selecteren** pagina:</span><span class="sxs-lookup"><span data-stu-id="82081-146">On the **Select a wizard to use for importing projects** page:</span></span>

   <span data-ttu-id="82081-147">a.</span><span class="sxs-lookup"><span data-stu-id="82081-147">a.</span></span> <span data-ttu-id="82081-148">Selecteer **importeren als een algemene project**.</span><span class="sxs-lookup"><span data-stu-id="82081-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="82081-149">b.</span><span class="sxs-lookup"><span data-stu-id="82081-149">b.</span></span> <span data-ttu-id="82081-150">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-150">Click **Next**.</span></span>

   ![Pagina 'Een wizard te gebruiken voor het importeren van de projecten selecteren'][CL07]

1. <span data-ttu-id="82081-152">Op de **importeren projecten** pagina:</span><span class="sxs-lookup"><span data-stu-id="82081-152">On the **Import Projects** page:</span></span>

   <span data-ttu-id="82081-153">a.</span><span class="sxs-lookup"><span data-stu-id="82081-153">a.</span></span> <span data-ttu-id="82081-154">Geef de projectnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="82081-154">Specify your project name.</span></span>
   
   <span data-ttu-id="82081-155">b.</span><span class="sxs-lookup"><span data-stu-id="82081-155">b.</span></span> <span data-ttu-id="82081-156">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="82081-156">Click **Finish**.</span></span>

   ![Pagina Projecten importeren][CL08]

1. <span data-ttu-id="82081-158">Als de opslagplaats met succes is gekloond, ziet u alle bestanden die worden vermeld in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="82081-158">When the repository is cloned successfully, you see all the files listed in Eclipse.</span></span>

   ![Lokale-opslagplaats][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="82081-160">Maak een Maven-project vanuit uw lokale opslagplaats</span><span class="sxs-lookup"><span data-stu-id="82081-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="82081-161">De versie die voorjaar Boot Docker-opslagplaats bevat een voltooide Maven-project dat u voor deze zelfstudie gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="82081-161">The Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="82081-162">Klik op **bestand** > **importeren**.</span><span class="sxs-lookup"><span data-stu-id="82081-162">Click **File** > **Import**.</span></span>

   ![De opdracht importeren in het menu bestand][CL01]

1. <span data-ttu-id="82081-164">Wanneer de **importeren** dialoogvenster wordt geopend:</span><span class="sxs-lookup"><span data-stu-id="82081-164">When the **Import** dialog box opens:</span></span>

   <span data-ttu-id="82081-165">a.</span><span class="sxs-lookup"><span data-stu-id="82081-165">a.</span></span> <span data-ttu-id="82081-166">Vouw **Maven**.</span><span class="sxs-lookup"><span data-stu-id="82081-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="82081-167">b.</span><span class="sxs-lookup"><span data-stu-id="82081-167">b.</span></span> <span data-ttu-id="82081-168">Selecteer **bestaande Maven-projecten**.</span><span class="sxs-lookup"><span data-stu-id="82081-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="82081-169">c.</span><span class="sxs-lookup"><span data-stu-id="82081-169">c.</span></span> <span data-ttu-id="82081-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-170">Click **Next**.</span></span>

   ![Dialoogvenster importeren][MV01]

1. <span data-ttu-id="82081-172">Op de **Maven-projecten** pagina:</span><span class="sxs-lookup"><span data-stu-id="82081-172">On the **Maven Projects** page:</span></span>

   <span data-ttu-id="82081-173">a.</span><span class="sxs-lookup"><span data-stu-id="82081-173">a.</span></span> <span data-ttu-id="82081-174">Voor **hoofdmap**, geef de **voltooid** map in uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="82081-174">For **Root Directory**, specify the **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="82081-175">b.</span><span class="sxs-lookup"><span data-stu-id="82081-175">b.</span></span> <span data-ttu-id="82081-176">Vouw de **Geavanceerd** uit en voer de naam van een aangepaste voor **naam sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="82081-176">Expand the **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="82081-177">c.</span><span class="sxs-lookup"><span data-stu-id="82081-177">c.</span></span> <span data-ttu-id="82081-178">Selecteer het selectievakje uit voor de **pom.xml** bestand in het project.</span><span class="sxs-lookup"><span data-stu-id="82081-178">Select the box for the **pom.xml** file in the project.</span></span>
   
   <span data-ttu-id="82081-179">d.</span><span class="sxs-lookup"><span data-stu-id="82081-179">d.</span></span> <span data-ttu-id="82081-180">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="82081-180">Click **Finish**.</span></span>

   ![Pagina maven-projecten][MV02]

1. <span data-ttu-id="82081-182">Als het Maven-project opent, ziet u een tweede die worden vermeld in Eclipse-project.</span><span class="sxs-lookup"><span data-stu-id="82081-182">When the Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Lokale Maven-project][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="82081-184">Uw app Spring opstarten maken met behulp van Maven</span><span class="sxs-lookup"><span data-stu-id="82081-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="82081-185">Selecteer het Maven-project in de Projectverkenner Eclipse.</span><span class="sxs-lookup"><span data-stu-id="82081-185">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="82081-186">Klik op **uitvoeren** > **uitvoeren als** > **Maven build**.</span><span class="sxs-lookup"><span data-stu-id="82081-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Opdrachten uit te voeren als Maven bouwen][BU01]

1. <span data-ttu-id="82081-188">Wanneer uw toepassing is is gebouwd, toont de status van het consolevenster.</span><span class="sxs-lookup"><span data-stu-id="82081-188">When your application is successfully built, the console window shows the status.</span></span>

   ![Geslaagde Maven build][BU02]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="82081-190">Uw web-app publiceren naar Azure met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="82081-190">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="82081-191">Selecteer het Maven-project in de Projectverkenner Eclipse.</span><span class="sxs-lookup"><span data-stu-id="82081-191">In the Eclipse Project Explorer, select the Maven project.</span></span>

1. <span data-ttu-id="82081-192">Klik op de Azure **publiceren** menu en klik vervolgens op **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="82081-192">Click the Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Als de opdracht Docker-Container publiceren][PU01]

1. <span data-ttu-id="82081-194">Wanneer de **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="82081-194">When the **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="82081-195">a.</span><span class="sxs-lookup"><span data-stu-id="82081-195">a.</span></span> <span data-ttu-id="82081-196">Voer de naam van een aangepaste Docker-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="82081-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="82081-197">b.</span><span class="sxs-lookup"><span data-stu-id="82081-197">b.</span></span> <span data-ttu-id="82081-198">Voor **artefact implementeren**, het pad opgeven naar de **gs-spring-boot-docker-0.1.0.jar** bestand dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="82081-198">For **Artifact to deploy**, specify the path to the **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Geef Docker-opties][PU02]

   <span data-ttu-id="82081-200">Eventuele bestaande Docker-hosts worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="82081-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="82081-201">Als u kiest voor het implementeren van een bestaande host, kunt u verder met stap 5.</span><span class="sxs-lookup"><span data-stu-id="82081-201">If you choose to deploy to an existing host, you can skip to step 5.</span></span> <span data-ttu-id="82081-202">Gebruik anders de volgende stappen uit voor het maken van een host:</span><span class="sxs-lookup"><span data-stu-id="82081-202">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="82081-203">a.</span><span class="sxs-lookup"><span data-stu-id="82081-203">a.</span></span> <span data-ttu-id="82081-204">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="82081-204">Click **Add**.</span></span>

      ![Een nieuwe Docker-host toevoegen][PU03]

   <span data-ttu-id="82081-206">b.</span><span class="sxs-lookup"><span data-stu-id="82081-206">b.</span></span> <span data-ttu-id="82081-207">Wanneer de **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u de standaardinstellingen accepteren of kunt u aangepaste instellingen voor uw nieuwe Docker-host.</span><span class="sxs-lookup"><span data-stu-id="82081-207">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="82081-208">(Zie voor gedetailleerde beschrijvingen van de verschillende instellingen [een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u hebt opgegeven welke instellingen u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="82081-208">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Geef opties voor Docker-host][PU04]

   <span data-ttu-id="82081-210">c.</span><span class="sxs-lookup"><span data-stu-id="82081-210">c.</span></span> <span data-ttu-id="82081-211">U kunt bestaande inloggegevens van een Azure sleutelkluis gebruiken of kunt u nieuwe Docker-aanmeldingsreferenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="82081-211">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="82081-212">Klik op **voltooien** wanneer u uw opties hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="82081-212">Click **Finish** when you have specified your options.</span></span>

      ![Geef referenties op Docker-host][PU05]

1. <span data-ttu-id="82081-214">Selecteer de Docker-host en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82081-214">Select your Docker host, and then click **Next**.</span></span>

   ![Selecteer de Docker-host wilt laten gebruiken][PU06]

1. <span data-ttu-id="82081-216">Op de laatste pagina van de **Docker-Container in Azure implementeren** dialoogvenster geeft u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="82081-216">On the last page of the **Deploying Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="82081-217">a.</span><span class="sxs-lookup"><span data-stu-id="82081-217">a.</span></span> <span data-ttu-id="82081-218">U kunt een aangepaste naam voor de container die als host voor uw Docker-container fungeert opgeven of u kunt de standaardwaarde accepteren.</span><span class="sxs-lookup"><span data-stu-id="82081-218">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="82081-219">b.</span><span class="sxs-lookup"><span data-stu-id="82081-219">b.</span></span> <span data-ttu-id="82081-220">Geef de TCP-poorten voor uw docker-host met behulp van de volgende syntaxis: *[externe poort]*:*[interne poort]*.</span><span class="sxs-lookup"><span data-stu-id="82081-220">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="82081-221">Bijvoorbeeld: **80:8080** Hiermee geeft u een externe poort 80 en de interne Spring opstarten standaardpoort 8080.</span><span class="sxs-lookup"><span data-stu-id="82081-221">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="82081-222">Als u uw interne poort (bijvoorbeeld door het bewerken van het bestand application.yml) aangepast hebt, moet u het poortnummer opgeven voor de juiste routering uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="82081-222">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="82081-223">c.</span><span class="sxs-lookup"><span data-stu-id="82081-223">c.</span></span> <span data-ttu-id="82081-224">Nadat u deze opties configureert, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="82081-224">After you configure these options, click **Finish**.</span></span>

   ![Een Docker-container in Azure implementeren][PU07]

1. <span data-ttu-id="82081-226">Wanneer de Toolkit Azure is gepubliceerd, de Azure Activity Log weergegeven **gepubliceerde** voor de status.</span><span class="sxs-lookup"><span data-stu-id="82081-226">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker-host is geïmplementeerd][PU08]

## <a name="next-steps"></a><span data-ttu-id="82081-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="82081-228">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="82081-229">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="82081-229">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="82081-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="82081-230">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="82081-231">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="82081-231">[Spring Framework]: https://spring.io/</span></span>

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
