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
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="fe368-103">Een app Spring opstarten publiceren als een Docker-container met behulp van hello Azure Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="fe368-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="fe368-104">Hallo [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="fe368-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="fe368-105">Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="fe368-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="fe368-106">[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.</span><span class="sxs-lookup"><span data-stu-id="fe368-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="fe368-107">Deze zelfstudie wordt u begeleid Hallo stappen toodeploy een toepassing Spring opstarten als een Docker-container tooMicrosoft Azure via hello Azure Toolkit voor Eclipse.</span><span class="sxs-lookup"><span data-stu-id="fe368-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for Eclipse.</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repository"></a><span data-ttu-id="fe368-108">Hallo standaard Spring Boot Docker opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="fe368-108">Clone hello default Spring Boot Docker repository</span></span>

### <a name="import-hello-public-repository"></a><span data-ttu-id="fe368-109">Importeren Hallo openbare opslagplaats</span><span class="sxs-lookup"><span data-stu-id="fe368-109">Import hello public repository</span></span>

<span data-ttu-id="fe368-110">Hallo doorlopen volgende stappen Hallo Spring Boot Docker-opslagplaats tooyour lokale computer met behulp van IntelliJ klonen.</span><span class="sxs-lookup"><span data-stu-id="fe368-110">hello following steps walk you through cloning hello Spring Boot Docker repository tooyour local computer by using IntelliJ.</span></span> <span data-ttu-id="fe368-111">Als u een opdrachtregel toouse wilt, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="fe368-111">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="fe368-112">Open de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="fe368-112">Open Eclipse.</span></span>

1. <span data-ttu-id="fe368-113">Klik op **bestand** > **importeren**.</span><span class="sxs-lookup"><span data-stu-id="fe368-113">Click **File** > **Import**.</span></span>

   ![Menu van bestand importeren][CL01]

1. <span data-ttu-id="fe368-115">Wanneer Hallo **importeren** dialoogvenster wordt geopend:</span><span class="sxs-lookup"><span data-stu-id="fe368-115">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="fe368-116">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-116">a.</span></span> <span data-ttu-id="fe368-117">Vouw **Git**.</span><span class="sxs-lookup"><span data-stu-id="fe368-117">Expand **Git**.</span></span>

   <span data-ttu-id="fe368-118">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-118">b.</span></span> <span data-ttu-id="fe368-119">Selecteer **projecten van Git**.</span><span class="sxs-lookup"><span data-stu-id="fe368-119">Select **Projects from Git**.</span></span>
   
   <span data-ttu-id="fe368-120">c.</span><span class="sxs-lookup"><span data-stu-id="fe368-120">c.</span></span> <span data-ttu-id="fe368-121">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-121">Click **Next**.</span></span>

   ![Dialoogvenster importeren][CL02]

1. <span data-ttu-id="fe368-123">Op Hallo **opslagplaats bron selecteren** pagina:</span><span class="sxs-lookup"><span data-stu-id="fe368-123">On hello **Select Repository Source** page:</span></span>

   <span data-ttu-id="fe368-124">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-124">a.</span></span> <span data-ttu-id="fe368-125">Selecteer **URI klonen**.</span><span class="sxs-lookup"><span data-stu-id="fe368-125">Select **Clone URI**.</span></span>
   
   <span data-ttu-id="fe368-126">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-126">b.</span></span> <span data-ttu-id="fe368-127">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-127">Click **Next**.</span></span>

   ![Repository Source pagina selecteren][CL03]

1. <span data-ttu-id="fe368-129">Op Hallo **bron Git-opslagplaats** pagina:</span><span class="sxs-lookup"><span data-stu-id="fe368-129">On hello **Source Git Repository** page:</span></span>

   <span data-ttu-id="fe368-130">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-130">a.</span></span> <span data-ttu-id="fe368-131">Voor **URI**, voer `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span><span class="sxs-lookup"><span data-stu-id="fe368-131">For **URI**, enter `https://github.com/spring-guides/gs-spring-boot-docker.git`.</span></span> <span data-ttu-id="fe368-132">Deze stap moet automatisch invullen Hallo **Host** en **opslagplaats pad** velden Hello waarden corrigeren.</span><span class="sxs-lookup"><span data-stu-id="fe368-132">This step should automatically populate hello **Host** and **Repository path** fields with hello correct values.</span></span>
   
   <span data-ttu-id="fe368-133">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-133">b.</span></span> <span data-ttu-id="fe368-134">Hallo Spring opstarten opslagplaats is openbaar, dus u moet geen tooenter uw Git-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="fe368-134">hello Spring Boot repository is public, so you should not have tooenter your Git username and password.</span></span>
   
   <span data-ttu-id="fe368-135">c.</span><span class="sxs-lookup"><span data-stu-id="fe368-135">c.</span></span> <span data-ttu-id="fe368-136">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-136">Click **Next**.</span></span>

   ![Bronpagina Git-opslagplaats][CL04]

1. <span data-ttu-id="fe368-138">Op Hallo **vertakking selectie** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-138">On hello **Branch Selection** page, click **Next**.</span></span>

   ![Selectie vertakkingpagina][CL05]

1. <span data-ttu-id="fe368-140">Op Hallo **lokale bestemming** pagina:</span><span class="sxs-lookup"><span data-stu-id="fe368-140">On hello **Local Destination** page:</span></span>

   <span data-ttu-id="fe368-141">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-141">a.</span></span> <span data-ttu-id="fe368-142">Hallo lokale map waar u uw lokale opslagplaats wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="fe368-142">Specify hello local folder where you want your local repo.</span></span>
   
   <span data-ttu-id="fe368-143">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-143">b.</span></span> <span data-ttu-id="fe368-144">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-144">Click **Next**.</span></span>

   ![Lokale doelpagina][CL06]

1. <span data-ttu-id="fe368-146">Op Hallo **een toouse wizard voor het importeren van de projecten selecteren** pagina:</span><span class="sxs-lookup"><span data-stu-id="fe368-146">On hello **Select a wizard toouse for importing projects** page:</span></span>

   <span data-ttu-id="fe368-147">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-147">a.</span></span> <span data-ttu-id="fe368-148">Selecteer **importeren als een algemene project**.</span><span class="sxs-lookup"><span data-stu-id="fe368-148">Select **Import as a general project**.</span></span>
   
   <span data-ttu-id="fe368-149">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-149">b.</span></span> <span data-ttu-id="fe368-150">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-150">Click **Next**.</span></span>

   ![Pagina 'Een toouse wizard voor het importeren van de projecten selecteren'][CL07]

1. <span data-ttu-id="fe368-152">Op Hallo **importeren projecten** pagina:</span><span class="sxs-lookup"><span data-stu-id="fe368-152">On hello **Import Projects** page:</span></span>

   <span data-ttu-id="fe368-153">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-153">a.</span></span> <span data-ttu-id="fe368-154">Geef de projectnaam van uw.</span><span class="sxs-lookup"><span data-stu-id="fe368-154">Specify your project name.</span></span>
   
   <span data-ttu-id="fe368-155">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-155">b.</span></span> <span data-ttu-id="fe368-156">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="fe368-156">Click **Finish**.</span></span>

   ![Pagina Projecten importeren][CL08]

1. <span data-ttu-id="fe368-158">Als het Hallo-opslagplaats met succes is gekloond, ziet u alle Hallo-bestanden die worden vermeld in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="fe368-158">When hello repository is cloned successfully, you see all hello files listed in Eclipse.</span></span>

   ![Lokale-opslagplaats][CL09]

### <a name="create-a-maven-project-from-your-local-repository"></a><span data-ttu-id="fe368-160">Maak een Maven-project vanuit uw lokale opslagplaats</span><span class="sxs-lookup"><span data-stu-id="fe368-160">Create a Maven project from your local repository</span></span>

<span data-ttu-id="fe368-161">Hallo Spring Boot Docker-opslagplaats bevat een voltooide Maven-project dat u voor deze zelfstudie gebruiken wilt.</span><span class="sxs-lookup"><span data-stu-id="fe368-161">hello Spring Boot Docker repository contains a completed Maven project, which you will use for this tutorial.</span></span> 

1. <span data-ttu-id="fe368-162">Klik op **bestand** > **importeren**.</span><span class="sxs-lookup"><span data-stu-id="fe368-162">Click **File** > **Import**.</span></span>

   ![Opdracht in menu Hallo-bestand importeren][CL01]

1. <span data-ttu-id="fe368-164">Wanneer Hallo **importeren** dialoogvenster wordt geopend:</span><span class="sxs-lookup"><span data-stu-id="fe368-164">When hello **Import** dialog box opens:</span></span>

   <span data-ttu-id="fe368-165">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-165">a.</span></span> <span data-ttu-id="fe368-166">Vouw **Maven**.</span><span class="sxs-lookup"><span data-stu-id="fe368-166">Expand **Maven**.</span></span>
   
   <span data-ttu-id="fe368-167">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-167">b.</span></span> <span data-ttu-id="fe368-168">Selecteer **bestaande Maven-projecten**.</span><span class="sxs-lookup"><span data-stu-id="fe368-168">Select **Existing Maven Projects**.</span></span>
   
   <span data-ttu-id="fe368-169">c.</span><span class="sxs-lookup"><span data-stu-id="fe368-169">c.</span></span> <span data-ttu-id="fe368-170">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-170">Click **Next**.</span></span>

   ![Dialoogvenster importeren][MV01]

1. <span data-ttu-id="fe368-172">Op Hallo **Maven-projecten** pagina:</span><span class="sxs-lookup"><span data-stu-id="fe368-172">On hello **Maven Projects** page:</span></span>

   <span data-ttu-id="fe368-173">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-173">a.</span></span> <span data-ttu-id="fe368-174">Voor **hoofdmap**, geef Hallo **voltooid** map in uw lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="fe368-174">For **Root Directory**, specify hello **complete** folder in your local repository.</span></span>
   
   <span data-ttu-id="fe368-175">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-175">b.</span></span> <span data-ttu-id="fe368-176">Vouw Hallo **Geavanceerd** uit en voer de naam van een aangepaste voor **naam sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="fe368-176">Expand hello **Advanced** section, and enter a custom name for **Name template**.</span></span>
   
   <span data-ttu-id="fe368-177">c.</span><span class="sxs-lookup"><span data-stu-id="fe368-177">c.</span></span> <span data-ttu-id="fe368-178">Selecteer Hallo-vak voor Hallo **pom.xml** bestand in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="fe368-178">Select hello box for hello **pom.xml** file in hello project.</span></span>
   
   <span data-ttu-id="fe368-179">d.</span><span class="sxs-lookup"><span data-stu-id="fe368-179">d.</span></span> <span data-ttu-id="fe368-180">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="fe368-180">Click **Finish**.</span></span>

   ![Pagina maven-projecten][MV02]

1. <span data-ttu-id="fe368-182">Als Hallo Maven-project opent, ziet u een tweede die worden vermeld in Eclipse-project.</span><span class="sxs-lookup"><span data-stu-id="fe368-182">When hello Maven project is opened successfully, you see a second project listed in Eclipse.</span></span>

   ![Lokale Maven-project][MV03]

## <a name="build-your-spring-boot-app-by-using-maven"></a><span data-ttu-id="fe368-184">Uw app Spring opstarten maken met behulp van Maven</span><span class="sxs-lookup"><span data-stu-id="fe368-184">Build your Spring Boot app by using Maven</span></span>

1. <span data-ttu-id="fe368-185">Selecteer in de Hallo Eclipse Projectverkenner, Hallo Maven-project.</span><span class="sxs-lookup"><span data-stu-id="fe368-185">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="fe368-186">Klik op **uitvoeren** > **uitvoeren als** > **Maven build**.</span><span class="sxs-lookup"><span data-stu-id="fe368-186">Click **Run** > **Run As** > **Maven build**.</span></span>

   ![Opdrachten toorun als Maven build][BU01]

1. <span data-ttu-id="fe368-188">Wanneer uw toepassing correct is samengesteld, bevat het consolevenster Hallo Hallo status.</span><span class="sxs-lookup"><span data-stu-id="fe368-188">When your application is successfully built, hello console window shows hello status.</span></span>

   ![Geslaagde Maven build][BU02]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="fe368-190">Uw web-app tooAzure publiceren met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="fe368-190">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="fe368-191">Selecteer in de Hallo Eclipse Projectverkenner, Hallo Maven-project.</span><span class="sxs-lookup"><span data-stu-id="fe368-191">In hello Eclipse Project Explorer, select hello Maven project.</span></span>

1. <span data-ttu-id="fe368-192">Klik op Hallo Azure **publiceren** menu en klik vervolgens op **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="fe368-192">Click hello Azure **Publish** menu, and then click **Publish as Docker Container**.</span></span>

   ![Als de opdracht Docker-Container publiceren][PU01]

1. <span data-ttu-id="fe368-194">Wanneer Hallo **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="fe368-194">When hello **Deploying Docker Container on Azure** dialog box appears:</span></span>

   <span data-ttu-id="fe368-195">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-195">a.</span></span> <span data-ttu-id="fe368-196">Voer de naam van een aangepaste Docker-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="fe368-196">Enter a custom Docker image name.</span></span>
   
   <span data-ttu-id="fe368-197">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-197">b.</span></span> <span data-ttu-id="fe368-198">Voor **artefact toodeploy**, geef Hallo pad toohello **gs-spring-boot-docker-0.1.0.jar** bestand dat u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fe368-198">For **Artifact toodeploy**, specify hello path toohello **gs-spring-boot-docker-0.1.0.jar** file you just built.</span></span>

   ![Geef Docker-opties][PU02]

   <span data-ttu-id="fe368-200">Eventuele bestaande Docker-hosts worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fe368-200">Any existing Docker hosts are displayed.</span></span> 

1. <span data-ttu-id="fe368-201">Als u toodeploy tooan bestaande host kiest, kunt u toostep 5 overslaan.</span><span class="sxs-lookup"><span data-stu-id="fe368-201">If you choose toodeploy tooan existing host, you can skip toostep 5.</span></span> <span data-ttu-id="fe368-202">Gebruik anders Hallo stappen toocreate een host te volgen:</span><span class="sxs-lookup"><span data-stu-id="fe368-202">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="fe368-203">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-203">a.</span></span> <span data-ttu-id="fe368-204">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="fe368-204">Click **Add**.</span></span>

      ![Een nieuwe Docker-host toevoegen][PU03]

   <span data-ttu-id="fe368-206">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-206">b.</span></span> <span data-ttu-id="fe368-207">Wanneer Hallo **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u tooaccept Hallo standaardwaarden of kunt u aangepaste instellingen voor uw nieuwe Docker-host.</span><span class="sxs-lookup"><span data-stu-id="fe368-207">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="fe368-208">(Zie voor gedetailleerde beschrijvingen van Hallo diverse instellingen [een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u welke instellingen toouse hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fe368-208">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Geef opties voor Docker-host][PU04]

   <span data-ttu-id="fe368-210">c.</span><span class="sxs-lookup"><span data-stu-id="fe368-210">c.</span></span> <span data-ttu-id="fe368-211">U kunt bestaande aanmeldingsreferenties toouse kiezen uit een Azure sleutelkluis, of u kunt tooenter nieuwe Docker-aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="fe368-211">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="fe368-212">Klik op **voltooien** wanneer u uw opties hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="fe368-212">Click **Finish** when you have specified your options.</span></span>

      ![Geef referenties op Docker-host][PU05]

1. <span data-ttu-id="fe368-214">Selecteer de Docker-host en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fe368-214">Select your Docker host, and then click **Next**.</span></span>

   ![Selecteer Docker host toouse][PU06]

1. <span data-ttu-id="fe368-216">Op de laatste pagina Hallo Hallo **Docker-Container in Azure implementeren** dialoogvenster geeft u de Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="fe368-216">On hello last page of hello **Deploying Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="fe368-217">a.</span><span class="sxs-lookup"><span data-stu-id="fe368-217">a.</span></span> <span data-ttu-id="fe368-218">U kunt toospecify een aangepaste naam voor het Hallo-container die als host voor uw Docker-container fungeert of kunt u de standaard Hallo accepteren.</span><span class="sxs-lookup"><span data-stu-id="fe368-218">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="fe368-219">b.</span><span class="sxs-lookup"><span data-stu-id="fe368-219">b.</span></span> <span data-ttu-id="fe368-220">Voer Hallo TCP-poorten voor de docker-host met behulp van de volgende syntaxis Hallo: *[externe poort]*:*[interne poort]*.</span><span class="sxs-lookup"><span data-stu-id="fe368-220">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="fe368-221">Bijvoorbeeld: **80:8080** geeft een externe poort 80 en Hallo interne Spring opstarten standaardpoort 8080.</span><span class="sxs-lookup"><span data-stu-id="fe368-221">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="fe368-222">Als u uw interne poort (bijvoorbeeld door het bewerken van Hallo application.yml-bestand) aangepast hebt, moet u toospecify Hallo-poortnummer voor de juiste routering toooccur Hallo in Azure.</span><span class="sxs-lookup"><span data-stu-id="fe368-222">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="fe368-223">c.</span><span class="sxs-lookup"><span data-stu-id="fe368-223">c.</span></span> <span data-ttu-id="fe368-224">Nadat u deze opties configureert, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="fe368-224">After you configure these options, click **Finish**.</span></span>

   ![Een Docker-container in Azure implementeren][PU07]

1. <span data-ttu-id="fe368-226">Wanneer hello Azure Toolkit is gepubliceerd, geeft Azure Activity Log Hallo **gepubliceerde** voor Hallo status.</span><span class="sxs-lookup"><span data-stu-id="fe368-226">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Docker-host is geïmplementeerd][PU08]

## <a name="next-steps"></a><span data-ttu-id="fe368-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fe368-228">Next steps</span></span>

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
