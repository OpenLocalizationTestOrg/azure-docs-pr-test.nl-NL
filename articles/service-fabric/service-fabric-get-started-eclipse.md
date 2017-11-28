---
title: Azure-Service Fabric-invoegtoepassing voor Eclipse | Microsoft Docs
description: Aan de slag met de Service Fabric- invoegtoepassing voor Eclipse.
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 98c1b99972b9ad7a396d72b98e727286f6822e42
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="b8e4a-103">Service Fabric-invoegtoepassing voor de ontwikkeling van Eclipse Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="b8e4a-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="b8e4a-104">Eclipse is een van de meest gebruikte Integrated Development Environments (IDE's) voor Java-ontwikkelaars.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-104">Eclipse is one of the most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="b8e4a-105">In dit artikel wordt beschreven hoe u een Eclipse-ontwikkelomgeving instelt voor gebruik met Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-105">In this article, we describe how to set up your Eclipse development environment to work with Azure Service Fabric.</span></span> <span data-ttu-id="b8e4a-106">Ontdek hoe u de Service Fabric-invoegtoepassing installeert en een Service Fabric-toepassing implementeert in een lokaal of extern Service Fabric-cluster in Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-106">Learn how to install the Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application to a local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-the-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="b8e4a-107">De Service Fabric-invoegtoepassing installeren of bijwerken in Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="b8e4a-107">Install or update the Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="b8e4a-108">U kunt een Service Fabric-invoegtoepassing in Eclipse installeren.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="b8e4a-109">De invoegtoepassing vereenvoudigt het proces voor het maken en implementeren van Java-services.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-109">The plug-in can help simplify the process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="b8e4a-110">Zorg ervoor dat u de nieuwste versie van Eclipse Neon en de nieuwste versie van Buildship (1.0.17 of hoger) hebt geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-110">Ensure that you have the latest version of Eclipse Neon and the latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="b8e4a-111">U kunt de versies van geïnstalleerde onderdelen controleren door in Eclipse Neon **Help** > **Installation Details** te kiezen.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-111">To check the versions of installed components, in Eclipse Neon, go to **Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="b8e4a-112">Zie [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update] (Eclipse Buildship: Eclipse-invoegtoepassingen voor Gradle) als u Buildship wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-112">To update Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="b8e4a-113">Als u updates voor Eclipse Neon wilt zoeken en installeren, gaat u naar **Help** > **Check for Updates**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-113">To check for and install updates for Eclipse Neon, go to **Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="b8e4a-114">Als u de Service Fabric-invoegtoepassing wilt installeren, gaat u in Eclipse Neon naar **Help** > **Install New Software**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-114">To install the Service Fabric plug-in, in Eclipse Neon, go to **Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="b8e4a-115">Geef in het vak **Work with** **http://dl.microsoft.com/eclipse** op.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-115">In the **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="b8e4a-116">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-116">Click **Add**.</span></span>

         ![De Service Fabric-invoegtoepassing voor Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="b8e4a-118">Selecteer de Fabric Service-invoegtoepassing en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-118">Select the Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="b8e4a-119">Voer de installatiestappen uit en accepteer de licentievoorwaarden voor Microsoft-software.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-119">Complete the installation steps, and then accept the Microsoft Software License Terms.</span></span>

<span data-ttu-id="b8e4a-120">Als u de Service Fabric-invoegtoepassing al hebt geïnstalleerd, controleert u of u de meest recente versie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-120">If you already have the Service Fabric plug-in installed, make sure that you have the latest version.</span></span> <span data-ttu-id="b8e4a-121">Ga naar **Help** > **Installation Details** om te controleren of er updates beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-121">To check for available updates, go to **Help** > **Installation Details**.</span></span> <span data-ttu-id="b8e4a-122">Selecteer Service Fabric in de lijst met geïnstalleerde invoegtoepassingen en klik op **Update**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-122">In the list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="b8e4a-123">Beschikbare updates worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="b8e4a-124">Als de installatie of update van de Service Fabric-invoegtoepassing traag verloopt, kan dit het gevolg zijn van een instelling in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-124">If installing or updating the Service Fabric plug-in is slow, it might be due to an Eclipse setting.</span></span> <span data-ttu-id="b8e4a-125">Eclipse verzamelt metagegevens over alle wijzigingen in updatesites die zijn geregistreerd bij uw exemplaar van Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-125">Eclipse collects metadata on all changes to update sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="b8e4a-126">Als u het proces voor het controleren op en installeren van updates van Service Fabric-invoegtoepassingen wilt versnellen, gaat u naar **Available Software Sites**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-126">To speed up the process of checking for and installing a Service Fabric plug-in update, go to **Available Software Sites**.</span></span> <span data-ttu-id="b8e4a-127">Schakel de selectievakjes uit voor alle sites, behalve voor de site die naar de locatie van de Fabric Service-invoegtoepassing wijst (http://dl.microsoft.com/eclipse/azure/servicefabric).</span><span class="sxs-lookup"><span data-stu-id="b8e4a-127">Clear the check boxes for all sites except for the one that points to the Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="b8e4a-128">Een Service Fabric-toepassing maken in Eclipse</span><span class="sxs-lookup"><span data-stu-id="b8e4a-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="b8e4a-129">Ga in Eclipse Neon naar **File** > **New** > **Other**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-129">In Eclipse Neon, go to **File** > **New** > **Other**.</span></span> <span data-ttu-id="b8e4a-130">Selecteer **Fabric Service Project** en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Nieuw Service Fabric-project pagina 1][create-application/p1]

2.  <span data-ttu-id="b8e4a-132">Voer een naam in voor het project en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Nieuw Service Fabric-project pagina 2][create-application/p2]

3.  <span data-ttu-id="b8e4a-134">Selecteer **Service Template** in de lijst met sjablonen.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-134">In the list of templates, select **Service Template**.</span></span> <span data-ttu-id="b8e4a-135">Selecteer het type servicesjabloon (Actor, Stateless, Container of Guest Binary) en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Nieuw Service Fabric-project pagina 3][create-application/p3]

4.  <span data-ttu-id="b8e4a-137">Voer de servicenaam en servicegegevens in en klik op **Finish**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-137">Enter the service name and service details, and then click **Finish**.</span></span>

    ![Nieuw Service Fabric-project pagina 4][create-application/p4]

5. <span data-ttu-id="b8e4a-139">Wanneer u uw eerste Service Fabric-project maakt, klikt u in het dialoogvenster **Open Associated Perspective** op **Yes**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-139">When you create your first Service Fabric project, in the **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Nieuw Service Fabric-project pagina 5][create-application/p5]

6.  <span data-ttu-id="b8e4a-141">Het nieuwe project ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-141">Your new project looks like this:</span></span>

    ![Nieuw Service Fabric-project pagina 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="b8e4a-143">Een Service Fabric-toepassing maken en implementeren in Eclipse</span><span class="sxs-lookup"><span data-stu-id="b8e4a-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="b8e4a-144">Klik met de rechtermuisknop op de nieuwe Service Fabric-toepassing en selecteer **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Snelmenu van Service Fabric][publish/RightClick]

2. <span data-ttu-id="b8e4a-146">Selecteer de gewenste optie in het submenu:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-146">In the submenu, select the option you want:</span></span>
    -   <span data-ttu-id="b8e4a-147">Klik op **Build Application** als u de toepassing wilt maken zonder op te schonen.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-147">To build the application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="b8e4a-148">Klik op **Rebuild Application** als u een schone build van de toepassing wilt maken.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-148">To do a clean build of the application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="b8e4a-149">Klik op **Clean Application** als u de gebouwde artefacts uit de toepassing wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-149">To clean the application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="b8e4a-150">Vanuit dit menu kunt u de toepassing ook implementeren, de implementatie ervan verwijderen en de toepassing publiceren:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="b8e4a-151">Klik op **Deploy Application** als u wilt implementeren naar het lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-151">To deploy to your local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="b8e4a-152">Selecteer in het dialoogvenster **Publish Application** een publicatieprofiel:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-152">In the **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="b8e4a-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="b8e4a-153">**Local.json**</span></span>
        -  <span data-ttu-id="b8e4a-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="b8e4a-154">**Cloud.json**</span></span>

     <span data-ttu-id="b8e4a-155">Deze JSON-bestanden (JavaScript Object Notation) bevatten informatie (zoals verbindingseindpunten en beveiligingsgegevens) die nodig zijn om verbinding te maken met het lokale cluster of het cloudcluster (Azure).</span><span class="sxs-lookup"><span data-stu-id="b8e4a-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required to connect to your local or cloud (Azure) cluster.</span></span>

  ![Service Fabric-menu Publish][publish/Publish]

<span data-ttu-id="b8e4a-157">U kunt de Service Fabric-toepassing ook implementeren met behulp van Eclipse-uitvoerconfiguraties.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-157">An alternate way to deploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="b8e4a-158">Ga naar **Run** > **Run Configurations**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-158">Go to **Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="b8e4a-159">Selecteer onder **Gradle Project** de uitvoerconfiguratie **ServiceFabricDeployer**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-159">Under **Gradle Project**, select the **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="b8e4a-160">Klik in het rechterdeelvenster op het tabblad **Arguments** en selecteer bij **publishProfile** de optie **local** of **cloud**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-160">In the right pane, on the **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="b8e4a-161">De standaardinstelling is **local**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-161">The default is **local**.</span></span> <span data-ttu-id="b8e4a-162">Selecteer **cloud** voor een implementatie in een extern of cloudcluster.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-162">To deploy to a remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="b8e4a-163">Bewerk **Local.json** of **Cloud.json** als dat nodig is om ervoor te zorgen dat de juiste informatie in de publicatieprofielen wordt ingevuld.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-163">To ensure that the proper information is populated in the publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="b8e4a-164">U kunt eindpuntdetails en beveiligingsreferenties toevoegen of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="b8e4a-165">Zorg ervoor dat **Working Directory** wijst naar de toepassing die u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-165">Ensure that **Working Directory** points to the application you want to deploy.</span></span> <span data-ttu-id="b8e4a-166">Als u de toepassing wilt wijzigen, klikt u op de knop **Workspace** en selecteert u de gewenste toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-166">To change the application, click the **Workspace** button, and then select the application you want.</span></span>
  6.    <span data-ttu-id="b8e4a-167">Klik op **Apply** en vervolgens op **Run**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="b8e4a-168">De toepassing is binnen enkele ogenblikken gemaakt en geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="b8e4a-169">U kunt de implementatiestatus controleren in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-169">You can monitor the deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-to-your-service-fabric-application"></a><span data-ttu-id="b8e4a-170">Een Service Fabric-service toevoegen aan uw Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="b8e4a-170">Add a Service Fabric service to your Service Fabric application</span></span>

<span data-ttu-id="b8e4a-171">Voer de volgende stappen uit als u een Service Fabric-service aan een bestaande Service Fabric-toepassing wilt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-171">To add a Service Fabric service to an existing Service Fabric application, do the following steps:</span></span>

1.  <span data-ttu-id="b8e4a-172">Klik met de rechtermuisknop op het project waaraan u een service wilt toevoegen en klik vervolgens op **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-172">Right-click the project you want to add a service to, and then click **Service Fabric**.</span></span>

    ![Service aan Service Fabric toevoegen pagina 1][add-service/p1]

2.  <span data-ttu-id="b8e4a-174">Klik op **Add Service Fabric Service** en voer de stappen uit om een service aan het project toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-174">Click **Add Service Fabric Service**, and complete the set of steps to add a service to the project.</span></span>
3.  <span data-ttu-id="b8e4a-175">Selecteer de servicesjabloon die u aan het project wilt toevoegen en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-175">Select the service template you want to add to your project, and then click **Next**.</span></span>

    ![Service aan Service Fabric toevoegen pagina 2][add-service/p2]

4.  <span data-ttu-id="b8e4a-177">Voer de servicenaam (en andere gevraagde informatie) in en klik op de knop **Add Service**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-177">Enter the service name (and other details, as needed), and then click the **Add Service** button.</span></span>  

    ![Service aan Service Fabric toevoegen pagina 3][add-service/p3]

5.  <span data-ttu-id="b8e4a-179">Nadat de service is toegevoegd, ziet de algehele projectstructuur er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b8e4a-179">After the service is added, your overall project structure looks similar to the following project:</span></span>

    ![Service aan Service Fabric toevoegen pagina 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="b8e4a-181">Manifestversies van uw Service Fabric Java-toepassing bewerken</span><span class="sxs-lookup"><span data-stu-id="b8e4a-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="b8e4a-182">Als u manifestversies wilt bewerken, klikt u met de rechtermuisknop op het project, gaat u naar **Service Fabric** en selecteert u **Edit Manifest Versions...** in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-182">To edit manifest versions, right click on the project, go to **Service Fabric** and select **Edit Manifest Versions...** from the menu dropdown.</span></span> <span data-ttu-id="b8e4a-183">In de wizard kunt u de manifestversies bijwerken voor het toepassingsmanifest, servicemanifest en de versies voor de pakketten **Code**, **Config** en **Data**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-183">In the wizard, you can update the manifest versions for application manifest, service manifest and the versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="b8e4a-184">Als u de optie **Automatically update application and service versions** inschakelt en vervolgens een versie bijwerkt, worden de manifestversies automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-184">If you check the option **Automatically update application and service versions** and then update a version, then the manifest versions will be automatically updated.</span></span> <span data-ttu-id="b8e4a-185">Als u bijvoorbeeld eerst het selectievakje inschakelt, vervolgens de versie van **Code** bijwerkt van 0.0.0 naar 0.0.1 en op **Finish** klikt, worden de versies van het servicemanifest en toepassingsmanifest automatisch bijgewerkt naar 0.0.1.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-185">To give an example, you first select the check-box, then update the version of **Code** version from 0.0.0 to 0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated to 0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="b8e4a-186">Uw Service Fabric Java-toepassing upgraden</span><span class="sxs-lookup"><span data-stu-id="b8e4a-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="b8e4a-187">Stel dat u voor een upgradescenario het project **App1** hebt gemaakt met behulp van de Service Fabric-invoegtoepassing in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-187">For an upgrade scenario, say you created the **App1** project by using the Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="b8e4a-188">U hebt dit vervolgens met behulp van de invoegtoepassing geïmplementeerd om een toepassing met de naam **fabric:/App1Application** te maken.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-188">You deployed it by using the plug-in to create an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="b8e4a-189">Het toepassingstype is **App1AppicationType** en de toepassingsversie is 1.0.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-189">The application type is **App1AppicationType**, and the application version is 1.0.</span></span> <span data-ttu-id="b8e4a-190">Nu wilt u een toepassingsupgrade uitvoeren zonder de beschikbaarheid van de toepassing te onderbreken.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-190">Now, you want to upgrade your application without interrupting availability.</span></span>

<span data-ttu-id="b8e4a-191">Breng eerst eventuele wijzigingen aan in de toepassing en bouw vervolgens de gewijzigde service opnieuw op.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-191">First, make any changes to your application, and then rebuild the modified service.</span></span> <span data-ttu-id="b8e4a-192">Werk het manifestbestand van de gewijzigde service (ServiceManifest.xml) bij met de bijgewerkte versies voor de service (en code, configuratie of gegevens, indien van toepassing).</span><span class="sxs-lookup"><span data-stu-id="b8e4a-192">Update the modified service’s manifest file (ServiceManifest.xml) with the updated versions for the service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="b8e4a-193">Wijzig ook het toepassingsmanifest (ApplicationManifest.xml) met het bijgewerkte versienummer voor de toepassing en de gewijzigde service.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-193">Also, modify the application’s manifest (ApplicationManifest.xml) with the updated version number for the application and the modified service.</span></span>  

<span data-ttu-id="b8e4a-194">Als u de toepassingsupgrade wilt uitvoeren met behulp van Eclipse Neon, kunt u een dubbel uitvoerconfiguratieprofiel maken.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-194">To upgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="b8e4a-195">Vervolgens gebruikt u dit om de toepassingsupgrade uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-195">Then, use it to upgrade your application as needed.</span></span>

1.  <span data-ttu-id="b8e4a-196">Ga naar **Run** > **Run Configurations**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-196">Go to **Run** > **Run Configurations**.</span></span> <span data-ttu-id="b8e4a-197">Klik in het linkerdeelvenster op de kleine pijl, links van **Gradle Project**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-197">In the left pane, click the small arrow to the left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="b8e4a-198">Klik met de rechtermuisknop op **ServiceFabricDeployer** en selecteer **Duplicate**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="b8e4a-199">Voer een nieuwe naam in voor deze configuratie, bijvoorbeeld **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="b8e4a-200">Ga in het rechterdeelvenster naar het tabblad **Arguments** en wijzig **-Pconfig='deploy'** in **-Pconfig=upgrade**. Klik vervolgens op **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-200">In the right panel, on the **Arguments** tab, change **-Pconfig='deploy'** to **-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="b8e4a-201">Met dit proces wordt een uitvoerconfiguratieprofiel gemaakt en opgeslagen dat u op elk gewenst moment kunt gebruiken om een upgrade van uw toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-201">This process creates and saves a run configuration profile you can use at any time to upgrade your application.</span></span> <span data-ttu-id="b8e4a-202">Hiermee wordt ook de laatst bijgewerkte versie van het toepassingstype opgehaald uit het manifest-bestand van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-202">It also gets the latest updated application type version from the application manifest file.</span></span>

<span data-ttu-id="b8e4a-203">De toepassingsupgrade duurt enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-203">The application upgrade takes a few minutes.</span></span> <span data-ttu-id="b8e4a-204">U kunt de upgrade van de toepassing bewaken in Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-204">You can monitor the application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-to-be-used-with-maven"></a><span data-ttu-id="b8e4a-205">Oude Service Fabric Java-toepassingen migreren die moeten worden gebruikt met Maven</span><span class="sxs-lookup"><span data-stu-id="b8e4a-205">Migrating old Service Fabric Java applications to be used with Maven</span></span>
<span data-ttu-id="b8e4a-206">We hebben onlangs de bibliotheken van Java Service Fabric verplaatst van de Service Fabric Java SDK naar de Maven-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK to Maven repository.</span></span> <span data-ttu-id="b8e4a-207">De nieuwe toepassingen die u genereert met behulp van Eclipse produceren projecten die u zonder problemen kunt gebruiken met Maven. Uw bestaande stateless Service Fabric- of Java-actortoepassingen zult u echter moeten bijwerken om ze te laten werken met de Service Fabric Java-afhankelijkheden van Maven. Deze oudere toepassingen maken namelijk nog gebruik van de Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-207">While the new applications you generate using Eclipse, will generate latest updated projects (which will be able to work with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using the Service Fabric Java SDK earlier, to use the Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="b8e4a-208">Volg [deze stappen](service-fabric-migrate-old-javaapp-to-use-maven.md) om te controleren of een oudere toepassing werkt met Maven.</span><span class="sxs-lookup"><span data-stu-id="b8e4a-208">Please follow the steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) to ensure your older application works with Maven.</span></span>

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
