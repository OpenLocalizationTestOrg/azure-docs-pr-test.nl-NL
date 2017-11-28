---
title: Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ | Microsoft Docs
description: Informatie over het publiceren van een web-app naar Microsoft Azure als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ.
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
ms.openlocfilehash: b771238934183c953615ac33c42a275d80657556
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="publish-a-spring-boot-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="c037e-103">Een app Spring opstarten publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c037e-103">Publish a Spring Boot app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="c037e-104">De [Spring Framework] is een open source-oplossing waarmee ontwikkelaars van Java op bedrijfsniveau toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="c037e-104">The [Spring Framework] is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="c037e-105">Een van de meer populaire projecten die is gebaseerd op deze platform is [Spring Boot], waarmee u een vereenvoudigde benadering voor het maken van zelfstandige Java-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c037e-105">One of the more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating standalone Java applications.</span></span>

<span data-ttu-id="c037e-106">[Docker] is een open source-oplossing waarmee ontwikkelaars automatiseren implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in containers.</span><span class="sxs-lookup"><span data-stu-id="c037e-106">[Docker] is an open-source solution that helps developers automate the deployment, scaling, and management of their applications that are running in containers.</span></span>

<span data-ttu-id="c037e-107">Deze zelfstudie leert u de stappen voor het implementeren van een toepassing Spring opstarten als een Docker-container met Microsoft Azure met behulp van de Azure-Toolkit voor IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c037e-107">This tutorial walks you through the steps to deploy a Spring Boot application as a Docker container to Microsoft Azure by using the Azure Toolkit for IntelliJ.</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="clone-the-default-spring-boot-docker-repo"></a><span data-ttu-id="c037e-108">Kloon de standaard Spring Boot Docker-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="c037e-108">Clone the default Spring Boot Docker repo</span></span>

<span data-ttu-id="c037e-109">De volgende stappen maakt u via de Spring Boot Docker-opslagplaats met behulp van IntelliJ klonen.</span><span class="sxs-lookup"><span data-stu-id="c037e-109">The following steps walk you through cloning the Spring Boot Docker repo by using IntelliJ.</span></span> <span data-ttu-id="c037e-110">Als u wilt een opdrachtregel te gebruiken, Zie [implementeren van een toepassing Spring opstarten op Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span><span class="sxs-lookup"><span data-stu-id="c037e-110">If you want to use a command line, see [Deploy a Spring Boot application on Linux in Azure Container Service][Deploy Spring Boot on Linux in ACS].</span></span>

1. <span data-ttu-id="c037e-111">Open IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="c037e-111">Open IntelliJ.</span></span>

1. <span data-ttu-id="c037e-112">Selecteer op het welkomstscherm van de **GitHub** optie in de **uitchecken uit versiebeheer** lijst.</span><span class="sxs-lookup"><span data-stu-id="c037e-112">On the welcome screen, select the **GitHub** option in the **Check out from Version Control** list.</span></span>

   ![GitHub-optie voor versiebeheer][CL01]

1. <span data-ttu-id="c037e-114">Geef uw referenties als u wordt gevraagd om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="c037e-114">Enter your credentials if you are prompted to log in.</span></span>

   * <span data-ttu-id="c037e-115">Als u een gebruikersnaam en wachtwoord voor aanmelding bij GitHub:</span><span class="sxs-lookup"><span data-stu-id="c037e-115">If you are using a username/password to log in to GitHub:</span></span>

      ![In het dialoogvenster voor het invoeren van GitHub-gebruikersnaam en wachtwoord][CL02a]

   * <span data-ttu-id="c037e-117">Als u een token gebruikt voor aanmelding bij GitHub:</span><span class="sxs-lookup"><span data-stu-id="c037e-117">If you are using a token to log in to GitHub:</span></span>

      ![In het dialoogvenster voor het invoeren van een GitHub-token][CL02b]

1. <span data-ttu-id="c037e-119">Voer **https://github.com/spring-guides/gs-spring-boot-docker.git** opgeven voor de URL van de opslagplaats, uw lokale pad en de mapgegevens en klik vervolgens op **kloon**.</span><span class="sxs-lookup"><span data-stu-id="c037e-119">Enter **https://github.com/spring-guides/gs-spring-boot-docker.git** for the repo URL, specify your local path and folder information, and then click **Clone**.</span></span>

   ![Dialoogvenster kloon-opslagplaats][CL03]

1. <span data-ttu-id="c037e-121">Wanneer u wordt gevraagd om een IntelliJ-project te maken, selecteert u **Nee**.</span><span class="sxs-lookup"><span data-stu-id="c037e-121">When you're prompted to create an IntelliJ project, select **No**.</span></span>

   ![Weigeren een IntelliJ-project maken][CL04]

1. <span data-ttu-id="c037e-123">Klik op de welkomstpagina op **Project importeren**.</span><span class="sxs-lookup"><span data-stu-id="c037e-123">On the welcome page, click **Import Project**.</span></span>

   ![Het project importeren][CL05]

1. <span data-ttu-id="c037e-125">Zoek het pad waar u de opslagplaats Spring opstarten gekloond, selecteert u de **voltooid** map onder de hoofdmap en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c037e-125">Locate the path where you cloned the Spring Boot repo, select the **complete** folder under the root, and then click **OK**.</span></span>

   ![Selecteer een map voor importeren][CL06]

1. <span data-ttu-id="c037e-127">Wanneer u wordt gevraagd, selecteert u **project maken van bestaande bronnen**.</span><span class="sxs-lookup"><span data-stu-id="c037e-127">When you're prompted, select **Create project from existing sources**.</span></span>

   ![Optie voor het maken van een project van bestaande bronnen][CL07]

1. <span data-ttu-id="c037e-129">Geef de projectnaam van uw of accepteer de standaardinstelling, controleert u het juiste pad naar de **voltooid** map en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c037e-129">Specify your project name or accept the default, verify the correct path to the **complete** folder, and then click **Next**.</span></span>

   ![Geef de naam van het project][CL08]

1. <span data-ttu-id="c037e-131">Alle mappen voor het importeren van aanpassen en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c037e-131">Customize any directories for importing, and then click **Next**.</span></span>

   ![Kies de mappen][CL09]

1. <span data-ttu-id="c037e-133">Bekijk de bibliotheken om te importeren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c037e-133">Review the libraries to import, and then click **Next**.</span></span>

   ![Bekijk de project-bibliotheken][CL10]

1. <span data-ttu-id="c037e-135">Structuur van de module bekijken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c037e-135">Review the module structure, and then click **Next**.</span></span>

   ![Bekijk de modulestructuur][CL11]

1. <span data-ttu-id="c037e-137">Geef uw JDK en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c037e-137">Specify your JDK, and then click **Next**.</span></span>

   ![Geef een JDK][CL12]

1. <span data-ttu-id="c037e-139">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c037e-139">Click **Finish**.</span></span>

   ![De knop Voltooien][CL13]

<span data-ttu-id="c037e-141">IntelliJ importeert de Spring Boot-app als een project en de structuur wordt weergegeven wanneer het importeren is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c037e-141">IntelliJ imports the Spring Boot app as a project and displays the structure when the import has finished.</span></span>

![Spring Boot-app in IntelliJ][CL14]

## <a name="build-your-spring-boot-app"></a><span data-ttu-id="c037e-143">Uw Spring opstart opbouwen app</span><span class="sxs-lookup"><span data-stu-id="c037e-143">Build your Spring Boot app</span></span>

### <a name="build-the-app-by-using-the-maven-pom"></a><span data-ttu-id="c037e-144">De app bouwen met behulp van de POM Maven</span><span class="sxs-lookup"><span data-stu-id="c037e-144">Build the app by using the Maven POM</span></span>

1. <span data-ttu-id="c037e-145">Open het werkvenster Maven als deze nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="c037e-145">Open the Maven tool window if it is not already opened.</span></span> <span data-ttu-id="c037e-146">Klik op **weergave** > **Windows hulpprogramma** > **Maven-projecten**.</span><span class="sxs-lookup"><span data-stu-id="c037e-146">Click **View** > **Tool Windows** > **Maven Projects**.</span></span>

   ![Hulpprogramma voor Windows en Maven-projecten opdrachten][BU01]

1. <span data-ttu-id="c037e-148">In het venster Maven-hulpprogramma met de rechtermuisknop op **pakket** en selecteer **uitvoeren Maven Build**.</span><span class="sxs-lookup"><span data-stu-id="c037e-148">In the Maven tool window, right-click **package** and select **Run Maven Build**.</span></span> <span data-ttu-id="c037e-149">(Als uw Maven-project niet automatisch weergegeven wordt, klikt u op de **opnieuw importeren** pictogram op de werkbalk Maven.)</span><span class="sxs-lookup"><span data-stu-id="c037e-149">(If your Maven project does not show up automatically, click the **Reimport** icon on the Maven toolbar.)</span></span>

   ![Build Maven-opdracht uitvoeren][BU02]

1. <span data-ttu-id="c037e-151">IntelliJ moet worden weergegeven in een **BUILD SUCCESS** wanneer uw app Spring Boot is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c037e-151">IntelliJ should display a **BUILD SUCCESS** message when your Spring Boot app is successfully created.</span></span>

   ![BUILD SUCCESS bericht][BU03]

### <a name="create-a-deployment-ready-artifact"></a><span data-ttu-id="c037e-153">Maken van een artefact klaar voor implementatie</span><span class="sxs-lookup"><span data-stu-id="c037e-153">Create a deployment-ready artifact</span></span>

<span data-ttu-id="c037e-154">Voor het publiceren van uw app Spring opstart, moet u een artefact implementatie gereed te maken.</span><span class="sxs-lookup"><span data-stu-id="c037e-154">To publish your Spring Boot app, you need to create a deployment-ready artifact.</span></span> <span data-ttu-id="c037e-155">Voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="c037e-155">Use the following steps:</span></span>

1. <span data-ttu-id="c037e-156">Open IntelliJ uw web-app-project.</span><span class="sxs-lookup"><span data-stu-id="c037e-156">Open your web app project in IntelliJ.</span></span>

1. <span data-ttu-id="c037e-157">Klik op **bestand**, en klik vervolgens op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="c037e-157">Click **File**, and then click **Project Structure**.</span></span>

   ![Opdracht voor project-structuur][ART01]

1. <span data-ttu-id="c037e-159">Klik op het groen plusteken (**+**) symbool een artefact toevoegen, klikt u op **JAR**, en klik vervolgens op **leeg**.</span><span class="sxs-lookup"><span data-stu-id="c037e-159">Click the green plus (**+**) symbol to add an artifact, click **JAR**, and then click **Empty**.</span></span>

   ![Toevoegen van een artefact][ART02]

1. <span data-ttu-id="c037e-161">Naam van uw artefacten terwijl u ervoor dat u niet de extensie "JAR" toevoegen en geef vervolgens de doelmap voor de uitvoer Maven.</span><span class="sxs-lookup"><span data-stu-id="c037e-161">Name your artifact while making sure not to add the ".jar" extension, and then specify the target folder for the Maven output.</span></span>

   ![Artefact-eigenschappen opgeven][ART03]

1. <span data-ttu-id="c037e-163">Maak een manifest voor uw artefacten (optioneel):</span><span class="sxs-lookup"><span data-stu-id="c037e-163">Create a manifest for your artifact (optional):</span></span>

   <span data-ttu-id="c037e-164">a.</span><span class="sxs-lookup"><span data-stu-id="c037e-164">a.</span></span> <span data-ttu-id="c037e-165">Klik op **Manifest maken**.</span><span class="sxs-lookup"><span data-stu-id="c037e-165">Click **Create Manifest**.</span></span>

      ![Klik op de knop maken Manifest][ART04a]

   <span data-ttu-id="c037e-167">b.</span><span class="sxs-lookup"><span data-stu-id="c037e-167">b.</span></span> <span data-ttu-id="c037e-168">Kies het standaardpad voor het artefact en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c037e-168">Choose the default path for the artifact, and then click **OK**.</span></span>

      ![Artefacten pad opgeven][ART04b]

   <span data-ttu-id="c037e-170">c.</span><span class="sxs-lookup"><span data-stu-id="c037e-170">c.</span></span> <span data-ttu-id="c037e-171">Klik op het weglatingsteken (**...** ) de hoofdklasse vinden.</span><span class="sxs-lookup"><span data-stu-id="c037e-171">Click the ellipsis (**...**) to locate the main class.</span></span>

      ![Zoek hoofdklasse][ART04c]

   <span data-ttu-id="c037e-173">d.</span><span class="sxs-lookup"><span data-stu-id="c037e-173">d.</span></span> <span data-ttu-id="c037e-174">Kies uw hoofdklasse en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c037e-174">Choose your main class, and then click **OK**.</span></span>

      ![Belangrijkste klasse op te geven][ART04d]

1. <span data-ttu-id="c037e-176">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c037e-176">Click **OK**.</span></span>

   ![Sluit het dialoogvenster Project-structuur][ART05]

> [!NOTE]
> <span data-ttu-id="c037e-178">Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op de website JetBrains.</span><span class="sxs-lookup"><span data-stu-id="c037e-178">For more information about creating artifacts in IntelliJ, see [Configuring Artifacts] on the JetBrains website.</span></span>
>

### <a name="build-the-artifact-for-deployment"></a><span data-ttu-id="c037e-179">Maken van het artefact voor implementatie</span><span class="sxs-lookup"><span data-stu-id="c037e-179">Build the artifact for deployment</span></span>

1. <span data-ttu-id="c037e-180">Klik op **bouwen**, en klik vervolgens op **artefacten**.</span><span class="sxs-lookup"><span data-stu-id="c037e-180">Click **Build**, and then click **Artifacts**.</span></span>

   ![Artefacten opdracht bouwen][BU04]

1. <span data-ttu-id="c037e-182">Wanneer de **bouwen artefact** contextmenu weergegeven, klikt u op **bouwen**.</span><span class="sxs-lookup"><span data-stu-id="c037e-182">When the **Build Artifact** context menu appears, click **Build**.</span></span>

   ![Contextmenu artefact bouwen][BU05]

<span data-ttu-id="c037e-184">IntelliJ het voltooide artefact voor uw app Spring opstarten moet worden weergegeven in het venster van het hulpprogramma project.</span><span class="sxs-lookup"><span data-stu-id="c037e-184">IntelliJ should display the completed artifact for your Spring Boot app in the project tool window.</span></span>

   ![Gemaakte artefact][BU06]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="c037e-186">Uw web-app publiceren naar Azure met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="c037e-186">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="c037e-187">Als u niet hebt aangemeld bij uw Azure-account, volg de stappen in [aanmelden instructies voor de Azure-Toolkit voor IntelliJ][Azure Sign In for IntelliJ].</span><span class="sxs-lookup"><span data-stu-id="c037e-187">If you have not signed in to your Azure account, follow the steps in [Sign-in instructions for the Azure Toolkit for IntelliJ][Azure Sign In for IntelliJ].</span></span>

1. <span data-ttu-id="c037e-188">In het venster van het hulpprogramma Projectverkenner met de rechtermuisknop op het project en selecteer vervolgens **Azure** > **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="c037e-188">In the Project Explorer tool window, right-click the project, and then select **Azure** > **Publish as Docker Container**.</span></span>

   ![Als de opdracht Docker-Container publiceren][PU01]

1. <span data-ttu-id="c037e-190">Wanneer de **Docker-Container in Azure implementeren** dialoogvenster wordt weergegeven, worden alle bestaande Docker-hosts weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c037e-190">When the **Deploy Docker Container on Azure** dialog box appears, any existing Docker hosts are displayed.</span></span> <span data-ttu-id="c037e-191">Als u kiest voor het implementeren van een bestaande host, kunt u doorgaan met stap 4.</span><span class="sxs-lookup"><span data-stu-id="c037e-191">If you choose to deploy to an existing host, you can skip to step 4.</span></span> <span data-ttu-id="c037e-192">Gebruik anders de volgende stappen uit voor het maken van een host:</span><span class="sxs-lookup"><span data-stu-id="c037e-192">Otherwise, use the following steps to create a host:</span></span>

   <span data-ttu-id="c037e-193">a.</span><span class="sxs-lookup"><span data-stu-id="c037e-193">a.</span></span> <span data-ttu-id="c037e-194">Klik op het groen plusteken (**+**) symbool.</span><span class="sxs-lookup"><span data-stu-id="c037e-194">Click the green plus (**+**) symbol.</span></span>

      ![Een nieuwe Docker-host toevoegen][PU02]

   <span data-ttu-id="c037e-196">b.</span><span class="sxs-lookup"><span data-stu-id="c037e-196">b.</span></span> <span data-ttu-id="c037e-197">Wanneer de **Docker-Host maken** dialoogvenster wordt weergegeven, kunt u de standaardinstellingen accepteren of kunt u aangepaste instellingen voor uw nieuwe Docker-host.</span><span class="sxs-lookup"><span data-stu-id="c037e-197">When the **Create Docker Host** dialog box appears, you can choose to accept the defaults, or you can specify any custom settings for your new Docker host.</span></span> <span data-ttu-id="c037e-198">(Zie voor gedetailleerde beschrijvingen van de verschillende instellingen [een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ][Publish Container with Azure Toolkit].) Klik op **volgende** wanneer u hebt opgegeven welke instellingen u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c037e-198">(For detailed descriptions of the various settings, see [Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ][Publish Container with Azure Toolkit].) Click **Next** when you have specified which settings to use.</span></span>

      ![Geef opties voor Docker-host][PU03a]

   <span data-ttu-id="c037e-200">c.</span><span class="sxs-lookup"><span data-stu-id="c037e-200">c.</span></span> <span data-ttu-id="c037e-201">U kunt bestaande inloggegevens van een Azure sleutelkluis gebruiken of kunt u nieuwe Docker-aanmeldingsreferenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="c037e-201">You can choose to use existing login credentials from an Azure key vault, or you can choose to enter new Docker login credentials.</span></span> <span data-ttu-id="c037e-202">Klik op **voltooien** wanneer u uw opties hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c037e-202">Click **Finish** when you have specified your options.</span></span>

      ![Geef referenties op Docker-host][PU03b]

1. <span data-ttu-id="c037e-204">Selecteer de Docker-host en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c037e-204">Select your Docker host, and then click **Next**.</span></span>

   ![Selecteer de Docker-host te gebruiken][PU04]

1. <span data-ttu-id="c037e-206">Op de laatste pagina van de **Docker-Container in Azure implementeren** dialoogvenster geeft u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="c037e-206">On the last page of the **Deploy Docker Container on Azure** dialog box, specify the following options:</span></span>

   <span data-ttu-id="c037e-207">a.</span><span class="sxs-lookup"><span data-stu-id="c037e-207">a.</span></span> <span data-ttu-id="c037e-208">U kunt een aangepaste naam voor de container die als host voor uw Docker-container fungeert opgeven of u kunt de standaardwaarde accepteren.</span><span class="sxs-lookup"><span data-stu-id="c037e-208">You can choose to specify a custom name for the container that will host your Docker container, or you can accept the default.</span></span>

   <span data-ttu-id="c037e-209">b.</span><span class="sxs-lookup"><span data-stu-id="c037e-209">b.</span></span> <span data-ttu-id="c037e-210">Geef de TCP-poorten voor uw docker-host met behulp van de volgende syntaxis: *[externe poort]*:*[interne poort]*.</span><span class="sxs-lookup"><span data-stu-id="c037e-210">Enter the TCP ports for your docker host by using the following syntax: *[external port]*:*[internal port]*.</span></span> <span data-ttu-id="c037e-211">Bijvoorbeeld: **80:8080** Hiermee geeft u een externe poort 80 en de interne Spring opstarten standaardpoort 8080.</span><span class="sxs-lookup"><span data-stu-id="c037e-211">For example, **80:8080** specifies an external port of 80 and the default internal Spring Boot port of 8080.</span></span>
   
      <span data-ttu-id="c037e-212">Als u uw interne poort (bijvoorbeeld door het bewerken van het bestand application.yml) aangepast hebt, moet u het poortnummer opgeven voor de juiste routering uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="c037e-212">If you have customized your internal port (for example, by editing the application.yml file), you need to specify the port number for the correct routing to occur in Azure.</span></span>

   <span data-ttu-id="c037e-213">c.</span><span class="sxs-lookup"><span data-stu-id="c037e-213">c.</span></span> <span data-ttu-id="c037e-214">Nadat u deze opties hebt geconfigureerd, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c037e-214">After you have configured these options, click **Finish**.</span></span>

   ![Een Docker-container in Azure implementeren][PU05]

1. <span data-ttu-id="c037e-216">Wanneer de Toolkit Azure is gepubliceerd, de Azure Activity Log weergegeven **gepubliceerde** voor de status.</span><span class="sxs-lookup"><span data-stu-id="c037e-216">When the Azure Toolkit has finished publishing, the Azure Activity Log displays **Published** for the status.</span></span>

   ![Docker-host is geïmplementeerd][PU06]

## <a name="next-steps"></a><span data-ttu-id="c037e-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c037e-218">Next steps</span></span>

[!INCLUDE [azure-toolkit-additional-resources](../includes/azure-toolkit-additional-resources.md)]

<span data-ttu-id="c037e-219">Zie voor meer informatie over aanvullende methoden voor het maken van opstarten Spring apps met behulp van IntelliJ, [Spring Boot-projecten maken](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) op de website JetBrains.</span><span class="sxs-lookup"><span data-stu-id="c037e-219">To learn about additional methods for creating Spring Boot apps by using IntelliJ, see [Creating Spring Boot Projects](https://www.jetbrains.com/help/idea/creating-spring-boot-projects.html) on the JetBrains website.</span></span>

<!-- URL List -->

[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Sign In for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
<span data-ttu-id="c037e-220">[artefacten configureren]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="c037e-220">[Configuring Artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>
[Deploy Spring Boot on Linux in ACS]:container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md
<span data-ttu-id="c037e-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="c037e-221">[Docker]: https://www.docker.com/</span></span>
[Publish Container with Azure Toolkit]: ./azure-toolkit-for-intellij-publish-as-docker-container.md
<span data-ttu-id="c037e-222">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="c037e-222">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="c037e-223">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="c037e-223">[Spring Framework]: https://spring.io/</span></span>

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
