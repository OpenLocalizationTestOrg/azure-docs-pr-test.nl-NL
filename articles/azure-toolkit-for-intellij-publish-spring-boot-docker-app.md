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
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="2f3b9-103">Een app Spring opstarten publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="2f3b9-103">Publish a Spring Boot app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="2f3b9-104">Hallo [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-104">hello [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="2f3b9-105">Een meer populaire Hallo-projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-105">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="2f3b9-106">[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-106">[Docker] is an open-source solution that helps developers automate hello deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="2f3b9-107">Deze zelfstudie wordt u begeleid Hallo stappen toodeploy een toepassing Spring opstarten als een Docker-container tooMicrosoft Azure via hello Azure Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-107">This tutorial walks you through hello steps toodeploy a Spring Boot application as a Docker container tooMicrosoft Azure by using hello Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-hello-default-spring-boot-docker-repo"></a><span data-ttu-id="2f3b9-108">Hallo standaard Spring Boot Docker opslagplaats klonen</span><span class="sxs-lookup"><span data-stu-id="2f3b9-108">Clone hello default Spring Boot Docker repo</span></span>

<span data-ttu-id="2f3b9-109">Hallo doorlopen volgende stappen Hallo Spring Boot Docker-opslagplaats met behulp van IntelliJ klonen.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-109">hello following steps walk you through cloning hello Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="2f3b9-110">Als u een opdrachtregel toouse wilt, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="2f3b9-110">If you want toouse a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="2f3b9-111">Open IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="2f3b9-112">Selecteer in het welkomstscherm Hallo Hallo **GitHub** optie in Hallo **uitchecken uit versiebeheer** lijst.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-112">On hello welcome screen, select hello **GitHub** option in hello **Check out from Version Control** list.</span></span>

   ![GitHub-optie voor versiebeheer][CL01]

1. <span data-ttu-id="2f3b9-114">Geef uw referenties als u na vragen aan gebruiker toolog in.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-114">Enter your credentials if you are prompted toolog in.</span></span>

   * <span data-ttu-id="2f3b9-115">Als u een gebruikersnaam en wachtwoord toolog in tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="2f3b9-115">If you are using a username/password toolog in tooGitHub:</span></span>

      ![In het dialoogvenster voor het invoeren van GitHub-gebruikersnaam en wachtwoord][CL02a]

   * <span data-ttu-id="2f3b9-117">Als u een token toolog in tooGitHub:</span><span class="sxs-lookup"><span data-stu-id="2f3b9-117">If you are using a token toolog in tooGitHub:</span></span>

      ![In het dialoogvenster voor het invoeren van een GitHub-token][CL02b]

1. <span data-ttu-id="2f3b9-119">Voer **https://github.com/spring-guides/gs-spring-boot-docker.git** uw lokale pad en de mapinformatie opgeven voor de URL van de opslagplaats hello, en klik vervolgens op **kloon**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for hello repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Dialoogvenster kloon-opslagplaats][CL03]

1. <span data-ttu-id="2f3b9-121">Wanneer u wordt gevraagd een IntelliJ-project, selecteer toocreate **Nee**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-121">When you're prompted toocreate an IntelliJ project, select **No**.</span></span>

   ![Een project IntelliJ toocreate weigeren][CL04]

1. <span data-ttu-id="2f3b9-123">Klik op de welkomstpagina Hallo **Project importeren**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-123">On hello welcome page, click **Import Project**.</span></span>

   ![Het project importeren][CL05]

1. <span data-ttu-id="2f3b9-125">Hallo-pad waar u Hallo Spring opstarten opslagplaats gekloond vinden, selecteer Hallo **voltooid** map onder de hoofdmap Hallo en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-125">Locate hello path where you cloned hello Spring Boot repo, select hello **complete** folder under hello root, and then click **OK**.</span></span>

   ![Selecteer een map voor importeren][CL06]

1. <span data-ttu-id="2f3b9-127">Wanneer u wordt gevraagd, selecteert u **project maken van bestaande bronnen**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Optie toocreate een project van bestaande bronnen][CL07]

1. <span data-ttu-id="2f3b9-129">Geef de projectnaam van uw of accepteer de standaardinstelling hello, Hallo pad toohello controleren **voltooid** map en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-129">Specify your project name or accept hello default, verify hello correct path toohello **complete** folder, and then click **Next**.</span></span>

   ![Hallo projectnaam opgeven][CL08]

1. <span data-ttu-id="2f3b9-131">Alle mappen voor het importeren van aanpassen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Kies de mappen][CL09]

1. <span data-ttu-id="2f3b9-133">Hallo-bibliotheken tooimport bekijken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-133">Review hello libraries tooimport, and then click **Next**.</span></span>

   ![Bekijk de project-bibliotheken][CL10]

1. <span data-ttu-id="2f3b9-135">Hallo Modulestructuur bekijken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-135">Review hello module structure, and then click **Next**.</span></span>

   ![Bekijk de modulestructuur][CL11]

1. <span data-ttu-id="2f3b9-137">Geef uw JDK en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-137">Specify your JDK, and then click **Next**.</span></span>

   ![Geef een JDK][CL12]

1. <span data-ttu-id="2f3b9-139">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-139">Click **Finish**.</span></span>

   ![De knop Voltooien][CL13]

<span data-ttu-id="2f3b9-141">IntelliJ hello Spring opstarten app als een project importeert en Hallo structuur wordt weergegeven wanneer Hallo importeren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-141">IntelliJ imports hello Spring Boot app as a project and displays hello structure when hello import has finished.</span></span>

![Spring Boot-app in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="2f3b9-143">Uw Spring opstart opbouwen app</span><span class="sxs-lookup"><span data-stu-id="2f3b9-143">Build your Spring Boot app</span></span>

### <a name="build-hello-app-by-using-hello-maven-pom"></a><span data-ttu-id="2f3b9-144">Hallo-app maken met behulp van Maven POM Hallo</span><span class="sxs-lookup"><span data-stu-id="2f3b9-144">Build hello app by using hello Maven POM</span></span>

1. <span data-ttu-id="2f3b9-145">Hallo Maven hulpprogramma venster openen als deze nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-145">Open hello Maven tool window if it is not already opened.</span></span> <span data-ttu-id="2f3b9-146">Klik op **weergave** > **Windows hulpprogramma** > **Maven-projecten**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Hulpprogramma voor Windows en Maven-projecten opdrachten][BU01]

1. <span data-ttu-id="2f3b9-148">Hallo Maven hulpprogramma venster met de rechtermuisknop op **pakket** en selecteer **uitvoeren Maven Build**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-148">In hello Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="2f3b9-149">(Als uw Maven-project niet automatisch weergegeven wordt, klikt u op Hallo **opnieuw importeren** pictogram op Hallo Maven-werkbalk.)</span><span class="sxs-lookup"><span data-stu-id="2f3b9-149">(If your Maven project does not show up automatically, click hello **Reimport** icon on hello Maven toolbar.)</span></span>

   ![Build Maven-opdracht uitvoeren][BU02]

1. <span data-ttu-id="2f3b9-151">IntelliJ moet worden weergegeven in een **BUILD SUCCESS** wanneer uw app Spring Boot is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![BUILD SUCCESS bericht][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="2f3b9-153">Maken van een artefact klaar voor implementatie</span><span class="sxs-lookup"><span data-stu-id="2f3b9-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="2f3b9-154">toopublish uw app Spring opstart, moet u een implementatie-ready artefact toocreate.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-154">toopublish your Spring Boot app, you need toocreate a deployment-ready artifact.</span></span> <span data-ttu-id="2f3b9-155">Gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f3b9-155">Use hello following steps:</span></span>

1. <span data-ttu-id="2f3b9-156">Open IntelliJ uw web-app-project.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="2f3b9-157">Klik op **bestand**, en klik vervolgens op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Opdracht voor project-structuur][ART01]

1. <span data-ttu-id="2f3b9-159">Klik op Hallo groen plus (**+**) tooadd een artefact symbool, klikt u op **JAR**, en klik vervolgens op **leeg**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-159">Click hello green plus (**+**) symbol tooadd an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Toevoegen van een artefact][ART02]

1. <span data-ttu-id="2f3b9-161">Naam van uw artefacten bij om ervoor te zorgen niet tooadd extensie 'JAR' Hallo en geef vervolgens de doelmap Hallo op Hallo Maven uitvoer.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-161">Name your artifact while making sure not tooadd hello ".jar" extension, and then specify hello target folder for hello Maven output.</span></span>

   ![Artefact-eigenschappen opgeven][ART03]

1. <span data-ttu-id="2f3b9-163">Maak een manifest voor uw artefacten (optioneel):</span><span class="sxs-lookup"><span data-stu-id="2f3b9-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="2f3b9-164">a.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-164">a.</span></span> <span data-ttu-id="2f3b9-165">Klik op **Manifest maken**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-165">Click **Create Manifest**.</span></span>

      ![Klik op Hallo Manifest maken][ART04a]

   <span data-ttu-id="2f3b9-167">b.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-167">b.</span></span> <span data-ttu-id="2f3b9-168">Kies Hallo standaardpad voor Hallo artefacten en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-168">Choose hello default path for hello artifact, and then click **OK**.</span></span>

      ![Artefacten pad opgeven][ART04b]

   <span data-ttu-id="2f3b9-170">c.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-170">c.</span></span> <span data-ttu-id="2f3b9-171">Klik op Hallo weglatingsteken (**...** ) toolocate Hallo hoofdklasse.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-171">Click hello ellipsis (**...**) toolocate hello main class.</span></span>

      ![Zoek hoofdklasse][ART04c]

   <span data-ttu-id="2f3b9-173">d.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-173">d.</span></span> <span data-ttu-id="2f3b9-174">Kies uw hoofdklasse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-174">Choose your main class, and then click **OK**.</span></span>

      ![Belangrijkste klasse op te geven][ART04d]

1. <span data-ttu-id="2f3b9-176">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-176">Click **OK**.</span></span>

   ![Hallo structuur Project dialoogvenster te sluiten][ART05]

> [!NOTE]
> <span data-ttu-id="2f3b9-178">Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op Hallo JetBrains website.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on hello JetBrains website.</span></span>
>

### <a name="build-hello-artifact-for-deployment"></a><span data-ttu-id="2f3b9-179">Hallo artefact voor implementatie maken</span><span class="sxs-lookup"><span data-stu-id="2f3b9-179">Build hello artifact for deployment</span></span>

1. <span data-ttu-id="2f3b9-180">Klik op **bouwen**, en klik vervolgens op **artefacten**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Artefacten opdracht bouwen][BU04]

1. <span data-ttu-id="2f3b9-182">Wanneer Hallo **bouwen artefact** contextmenu weergegeven, klikt u op **bouwen**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-182">When hello **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Contextmenu artefact bouwen][BU05]

<span data-ttu-id="2f3b9-184">IntelliJ artefact Hallo voltooid voor uw app Spring opstarten moet worden weergegeven in venster Hallo project-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-184">IntelliJ should display hello completed artifact for your Spring Boot app in hello project tool window.</span></span>

   ![Gemaakte artefact][BU06]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="2f3b9-186">Uw web-app tooAzure publiceren met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="2f3b9-186">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="2f3b9-187">Als u tooyour Azure-account niet hebt aangemeld, stappen Hallo in [aanmelden instructies voor hello Azure Toolkit voor IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="2f3b9-187">If you have not signed in tooyour Azure account, follow hello steps in [Sign-in instructions for hello Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="2f3b9-188">Hallo Projectverkenner hulpprogramma-venster met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Azure** > **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-188">In hello Project Explorer tool window, right-click hello project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Als de opdracht Docker-Container publiceren][PU01]

1. <span data-ttu-id="2f3b9-190">Wanneer Hallo **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven, worden alle bestaande Docker-hosts weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-190">When hello **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="2f3b9-191">Als u toodeploy tooan bestaande host kiest, kunt u toostep 4 overslaan.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-191">If you choose toodeploy tooan existing host, you can skip toostep 4.</span></span> <span data-ttu-id="2f3b9-192">Gebruik anders Hallo stappen toocreate een host te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f3b9-192">Otherwise, use hello following steps toocreate a host:</span></span>

   <span data-ttu-id="2f3b9-193">a.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-193">a.</span></span> <span data-ttu-id="2f3b9-194">Klik op Hallo groen plus (**+**) symbool.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-194">Click hello green plus (**+**) symbol.</span></span>

      ![Een nieuwe Docker-host toevoegen][PU02]

   <span data-ttu-id="2f3b9-196">b.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-196">b.</span></span> <span data-ttu-id="2f3b9-197">Wanneer Hallo **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u tooaccept Hallo standaardwaarden of kunt u aangepaste instellingen voor uw nieuwe Docker-host.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-197">When hello **Create Docker Host** dialog box appears, you can choose tooaccept hello defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="2f3b9-198">(Zie voor gedetailleerde beschrijvingen van Hallo diverse instellingen [een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u welke instellingen toouse hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-198">(For detailed descriptions of hello various settings, see [Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings toouse.</span></span>

      ![Geef opties voor Docker-host][PU03a]

   <span data-ttu-id="2f3b9-200">c.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-200">c.</span></span> <span data-ttu-id="2f3b9-201">U kunt bestaande aanmeldingsreferenties toouse kiezen uit een Azure sleutelkluis, of u kunt tooenter nieuwe Docker-aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-201">You can choose toouse existing login credentials from an Azure key vault, or you can choose tooenter new Docker login credentials.</span></span> <span data-ttu-id="2f3b9-202">Klik op **voltooien** wanneer u uw opties hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-202">Click **Finish** when you have specified your options.</span></span>

      ![Geef referenties op Docker-host][PU03b]

1. <span data-ttu-id="2f3b9-204">Selecteer de Docker-host en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-204">Select your Docker host, and then click **Next**.</span></span>

   ![Hallo Docker host toouse selecteren][PU04]

1. <span data-ttu-id="2f3b9-206">Op de laatste pagina Hallo Hallo **Docker-Container in Azure implementeren** dialoogvenster geeft u de Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="2f3b9-206">On hello last page of hello **Deploy Docker Container on Azure** dialog box, specify hello following options:</span></span>

   <span data-ttu-id="2f3b9-207">a.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-207">a.</span></span> <span data-ttu-id="2f3b9-208">U kunt toospecify een aangepaste naam voor het Hallo-container die als host voor uw Docker-container fungeert of kunt u de standaard Hallo accepteren.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-208">You can choose toospecify a custom name for hello container that will host your Docker container, or you can accept hello default.</span></span>

   <span data-ttu-id="2f3b9-209">b.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-209">b.</span></span> <span data-ttu-id="2f3b9-210">Voer Hallo TCP-poorten voor de docker-host met behulp van de volgende syntaxis Hallo: *[externe poort]*:*[interne poort]*.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-210">Enter hello TCP ports for your docker host by using hello following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="2f3b9-211">Bijvoorbeeld: **80:8080** geeft een externe poort 80 en Hallo interne Spring opstarten standaardpoort 8080.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-211">For example, **80:8080** specifies an external port of 80 and hello default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="2f3b9-212">Als u uw interne poort (bijvoorbeeld door het bewerken van Hallo application.yml-bestand) aangepast hebt, moet u toospecify Hallo-poortnummer voor de juiste routering toooccur Hallo in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-212">If you have customized your internal port (for example, by editing hello application.yml file), you need toospecify hello port number for hello correct routing toooccur in Azure.</span></span>

   <span data-ttu-id="2f3b9-213">c.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-213">c.</span></span> <span data-ttu-id="2f3b9-214">Nadat u deze opties hebt geconfigureerd, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-214">After you have configured these options, click **Finish**.</span></span>

   ![Een Docker-container in Azure implementeren][PU05]

1. <span data-ttu-id="2f3b9-216">Wanneer hello Azure Toolkit is gepubliceerd, geeft Azure Activity Log Hallo **gepubliceerde** voor Hallo status.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-216">When hello Azure Toolkit has finished publishing, hello Azure Activity Log displays **Published** for hello status.</span></span>

   ![Docker-host is geïmplementeerd][PU06]

## <a name="next-steps"></a><span data-ttu-id="2f3b9-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f3b9-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="2f3b9-219">toolearn over aanvullende methoden voor het maken van opstarten Spring apps met behulp van IntelliJ, Zie [Spring Boot-projecten maken](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) op Hallo JetBrains website.</span><span class="sxs-lookup"><span data-stu-id="2f3b9-219">toolearn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on hello JetBrains website.</span></span>

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
