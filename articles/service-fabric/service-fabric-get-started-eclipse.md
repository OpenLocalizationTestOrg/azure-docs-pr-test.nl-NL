---
title: Service Fabric-invoegtoepassing voor Eclipse aaaAzure | Microsoft Docs
description: Aan de slag met Hallo Service Fabric-invoegtoepassing voor Eclipse.
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
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a><span data-ttu-id="d9eaf-103">Service Fabric-invoegtoepassing voor de ontwikkeling van Eclipse Java-toepassingen</span><span class="sxs-lookup"><span data-stu-id="d9eaf-103">Service Fabric plug-in for Eclipse Java application development</span></span>
<span data-ttu-id="d9eaf-104">Eclipse is een van de meest gebruikte Hallo ontwikkelomgevingen (IDE's) voor Java-ontwikkelaars geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-104">Eclipse is one of hello most widely used integrated development environments (IDEs) for Java developers.</span></span> <span data-ttu-id="d9eaf-105">In dit artikel wordt beschreven hoe tooset van uw Eclipse development environment toowork met Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-105">In this article, we describe how tooset up your Eclipse development environment toowork with Azure Service Fabric.</span></span> <span data-ttu-id="d9eaf-106">Ontdek hoe tooinstall Hallo Service Fabric-invoegtoepassing, een Service Fabric-toepassing maken en implementeren van uw Service Fabric-toepassing tooa lokale of externe Service Fabric-cluster in Eclipse Neon.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-106">Learn how tooinstall hello Service Fabric plug-in, create a Service Fabric application, and deploy your Service Fabric application tooa local or remote Service Fabric cluster in Eclipse Neon.</span></span>

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a><span data-ttu-id="d9eaf-107">Installeren of bijwerken van Service Fabric-invoegtoepassing in Eclipse Neon Hallo</span><span class="sxs-lookup"><span data-stu-id="d9eaf-107">Install or update hello Service Fabric plug-in in Eclipse Neon</span></span>
<span data-ttu-id="d9eaf-108">U kunt een Service Fabric-invoegtoepassing in Eclipse installeren.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-108">You can install a Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="d9eaf-109">Hallo invoegtoepassing vereenvoudigen Hallo-proces voor het maken en implementeren van Java-services.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-109">hello plug-in can help simplify hello process of building and deploying Java services.</span></span>

1.  <span data-ttu-id="d9eaf-110">Zorg ervoor dat u de meest recente versie Hallo van Eclipse Neon en Hallo meest recente versie van Buildship (1.0.17 of een latere versie) geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-110">Ensure that you have hello latest version of Eclipse Neon and hello latest version of Buildship (1.0.17 or a later version) installed:</span></span>
    -   <span data-ttu-id="d9eaf-111">toocheck hello versies van geïnstalleerde onderdelen, in Eclipse Neon, gaat u te**Help** > **installatiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-111">toocheck hello versions of installed components, in Eclipse Neon, go too**Help** > **Installation Details**.</span></span>
    -   <span data-ttu-id="d9eaf-112">tooupdate Buildship, Zie [Eclipse Buildship: Eclipse-invoegtoepassingen voor Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="d9eaf-112">tooupdate Buildship, see [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>
    -   <span data-ttu-id="d9eaf-113">Ga te toocheck voor en installeren van updates voor de Eclipse-Neon**Help** > **controleren op Updates**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-113">toocheck for and install updates for Eclipse Neon, go too**Help** > **Check for Updates**.</span></span>

2.  <span data-ttu-id="d9eaf-114">tooinstall hello Service Fabric-invoegtoepassing in Eclipse Neon, gaat u te**Help** > **nieuwe Software installeren**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-114">tooinstall hello Service Fabric plug-in, in Eclipse Neon, go too**Help** > **Install New Software**.</span></span>
  1.    <span data-ttu-id="d9eaf-115">In Hallo **werken met** Voer **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-115">In hello **Work with** box, enter **http://dl.microsoft.com/eclipse**.</span></span>
  2.    <span data-ttu-id="d9eaf-116">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-116">Click **Add**.</span></span>

         ![De Service Fabric-invoegtoepassing voor Eclipse Neon][sf-eclipse-plugin-install]
  3.    <span data-ttu-id="d9eaf-118">Hallo Service Fabric-invoegtoepassing selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-118">Select hello Service Fabric plug-in, and then click **Next**.</span></span>
  4.    <span data-ttu-id="d9eaf-119">Hallo installatiestappen voltooien en accepteer de licentievoorwaarden voor Microsoft-Software Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-119">Complete hello installation steps, and then accept hello Microsoft Software License Terms.</span></span>

<span data-ttu-id="d9eaf-120">Als u al Hallo Service Fabric-invoegtoepassing is geïnstalleerd, zorg ervoor dat hebt u Hallo meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-120">If you already have hello Service Fabric plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="d9eaf-121">toocheck naar beschikbare updates te gaan**Help** > **installatiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-121">toocheck for available updates, go too**Help** > **Installation Details**.</span></span> <span data-ttu-id="d9eaf-122">Selecteer Service Fabric in Hallo lijst met geïnstalleerde invoegtoepassingen, en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-122">In hello list of installed plug-ins, select Service Fabric, and then click **Update**.</span></span> <span data-ttu-id="d9eaf-123">Beschikbare updates worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-123">Available updates will be installed.</span></span>

> [!NOTE]
> <span data-ttu-id="d9eaf-124">Als installeren of bijwerken van Service Fabric-invoegtoepassing Hallo traag is, mogelijk vanwege tooan Eclipse-instelling.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-124">If installing or updating hello Service Fabric plug-in is slow, it might be due tooan Eclipse setting.</span></span> <span data-ttu-id="d9eaf-125">Eclipse verzamelt metagegevens op alle wijzigingen tooupdate sites die zijn geregistreerd met uw Eclipse-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-125">Eclipse collects metadata on all changes tooupdate sites that are registered with your Eclipse instance.</span></span> <span data-ttu-id="d9eaf-126">toospeed Hallo-installatieproces van controleren en de installatie van een Service Fabric-invoegtoepassing update te gaan**beschikbare Software Sites**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-126">toospeed up hello process of checking for and installing a Service Fabric plug-in update, go too**Available Software Sites**.</span></span> <span data-ttu-id="d9eaf-127">Schakel de selectievakjes Hallo voor alle sites, met uitzondering van Hallo die toohello Service Fabric invoegtoepassing locatie (http://dl.microsoft.com/eclipse/azure/servicefabric wijst).</span><span class="sxs-lookup"><span data-stu-id="d9eaf-127">Clear hello check boxes for all sites except for hello one that points toohello Service Fabric plug-in location (http://dl.microsoft.com/eclipse/azure/servicefabric).</span></span>

## <a name="create-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="d9eaf-128">Een Service Fabric-toepassing maken in Eclipse</span><span class="sxs-lookup"><span data-stu-id="d9eaf-128">Create a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="d9eaf-129">Ga te in Eclipse-Neon**bestand** > **nieuw** > **andere**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-129">In Eclipse Neon, go too**File** > **New** > **Other**.</span></span> <span data-ttu-id="d9eaf-130">Selecteer **Fabric Service Project** en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-130">Select  **Service Fabric Project**, and then click **Next**.</span></span>

    ![Nieuw Service Fabric-project pagina 1][create-application/p1]

2.  <span data-ttu-id="d9eaf-132">Voer een naam in voor het project en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-132">Enter a name for your project, and then click **Next**.</span></span>

    ![Nieuw Service Fabric-project pagina 2][create-application/p2]

3.  <span data-ttu-id="d9eaf-134">Selecteer in de lijst met sjablonen Hallo **servicesjabloon**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-134">In hello list of templates, select **Service Template**.</span></span> <span data-ttu-id="d9eaf-135">Selecteer het type servicesjabloon (Actor, Stateless, Container of Guest Binary) en klik op **Next**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-135">Select your service template type (Actor, Stateless, Container, or Guest Binary), and then click **Next**.</span></span>

    ![Nieuw Service Fabric-project pagina 3][create-application/p3]

4.  <span data-ttu-id="d9eaf-137">Voer Hallo servicenaam en servicedetails en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-137">Enter hello service name and service details, and then click **Finish**.</span></span>

    ![Nieuw Service Fabric-project pagina 4][create-application/p4]

5. <span data-ttu-id="d9eaf-139">Wanneer u uw eerste Service Fabric-project maken in Hallo **openen die zijn gekoppeld perspectief** in het dialoogvenster klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-139">When you create your first Service Fabric project, in hello **Open Associated Perspective** dialog box, click **Yes**.</span></span>

    ![Nieuw Service Fabric-project pagina 5][create-application/p5]

6.  <span data-ttu-id="d9eaf-141">Het nieuwe project ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-141">Your new project looks like this:</span></span>

    ![Nieuw Service Fabric-project pagina 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a><span data-ttu-id="d9eaf-143">Een Service Fabric-toepassing maken en implementeren in Eclipse</span><span class="sxs-lookup"><span data-stu-id="d9eaf-143">Build and deploy a Service Fabric application in Eclipse</span></span>

1.  <span data-ttu-id="d9eaf-144">Klik met de rechtermuisknop op de nieuwe Service Fabric-toepassing en selecteer **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-144">Right-click your new Service Fabric application, and then select **Service Fabric**.</span></span>

    ![Snelmenu van Service Fabric][publish/RightClick]

2. <span data-ttu-id="d9eaf-146">Selecteer in vervolgmenu hello, Hallo-optie die u wilt:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-146">In hello submenu, select hello option you want:</span></span>
    -   <span data-ttu-id="d9eaf-147">toobuild hello toepassing zonder reinigen, klikt u op **toepassing bouwen**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-147">toobuild hello application without cleaning, click **Build Application**.</span></span>
    -   <span data-ttu-id="d9eaf-148">toodo leegmaken en opnieuw opbouwen van de toepassing hello, klikt u op **toepassing bouwen**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-148">toodo a clean build of hello application, click **Rebuild Application**.</span></span>
    -   <span data-ttu-id="d9eaf-149">tooclean hello toepassing van ingebouwde artefacten, klikt u op **schone toepassing**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-149">tooclean hello application of built artifacts, click **Clean Application**.</span></span>

3.  <span data-ttu-id="d9eaf-150">Vanuit dit menu kunt u de toepassing ook implementeren, de implementatie ervan verwijderen en de toepassing publiceren:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-150">From this menu, you also can deploy, undeploy, and publish your application:</span></span>
    -   <span data-ttu-id="d9eaf-151">toodeploy tooyour lokale cluster, klik op **toepassing implementeren**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-151">toodeploy tooyour local cluster, click **Deploy Application**.</span></span>
    -   <span data-ttu-id="d9eaf-152">In Hallo **toepassing publiceren** dialoogvenster Selecteer een publicatieprofiel:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-152">In hello **Publish Application** dialog box, select a publish profile:</span></span>
        -  <span data-ttu-id="d9eaf-153">**Local.json**</span><span class="sxs-lookup"><span data-stu-id="d9eaf-153">**Local.json**</span></span>
        -  <span data-ttu-id="d9eaf-154">**Cloud.json**</span><span class="sxs-lookup"><span data-stu-id="d9eaf-154">**Cloud.json**</span></span>

     <span data-ttu-id="d9eaf-155">Deze notatie JSON (JavaScript Object)-bestanden opgeslagen informatie (zoals verbindingseindpunten en beveiligingsgegevens) die is vereist tooconnect tooyour lokale cloud (Azure)-cluster.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-155">These JavaScript Object Notation (JSON) files store information (such as connection endpoints and security information) that is required tooconnect tooyour local or cloud (Azure) cluster.</span></span>

  ![Service Fabric-menu Publish][publish/Publish]

<span data-ttu-id="d9eaf-157">Een andere manier toodeploy Service Fabric-toepassing is via Eclipse uitvoeren configuraties.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-157">An alternate way toodeploy your Service Fabric application is by using Eclipse run configurations.</span></span>

  1.    <span data-ttu-id="d9eaf-158">Ga te**uitvoeren** > **configuratie uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-158">Go too**Run** > **Run Configurations**.</span></span>
  2.    <span data-ttu-id="d9eaf-159">Onder **Project met Gradle**, selecteer Hallo **ServiceFabricDeployer** configuratie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-159">Under **Gradle Project**, select hello **ServiceFabricDeployer** run configuration.</span></span>
  3.    <span data-ttu-id="d9eaf-160">In het rechterdeelvenster Hallo op Hallo **argumenten** tabblad voor **publishProfile**, selecteer **lokale** of **cloud**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-160">In hello right pane, on hello **Arguments** tab, for **publishProfile**, select **local** or **cloud**.</span></span>  <span data-ttu-id="d9eaf-161">Hallo standaardwaarde is **lokale**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-161">hello default is **local**.</span></span> <span data-ttu-id="d9eaf-162">toodeploy tooa externe of selecteer cloud cluster **cloud**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-162">toodeploy tooa remote or cloud cluster, select **cloud**.</span></span>
  4.    <span data-ttu-id="d9eaf-163">tooensure dat de juiste informatie Hallo is ingevuld in Hallo profielen publiceren, bewerken **Local.json** of **Cloud.json** indien nodig.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-163">tooensure that hello proper information is populated in hello publish profiles, edit **Local.json** or **Cloud.json** as needed.</span></span> <span data-ttu-id="d9eaf-164">U kunt eindpuntdetails en beveiligingsreferenties toevoegen of bijwerken.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-164">You can add or update endpoint details and security credentials.</span></span>
  5.    <span data-ttu-id="d9eaf-165">Zorg ervoor dat **werkmap** gewenste toodeploy toohello-toepassing verwijst.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-165">Ensure that **Working Directory** points toohello application you want toodeploy.</span></span> <span data-ttu-id="d9eaf-166">toochange toepassing hello, klikt u op Hallo **werkruimte** knop en selecteer vervolgens de gewenste Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-166">toochange hello application, click hello **Workspace** button, and then select hello application you want.</span></span>
  6.    <span data-ttu-id="d9eaf-167">Klik op **Apply** en vervolgens op **Run**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-167">Click **Apply**, and then click **Run**.</span></span>

<span data-ttu-id="d9eaf-168">De toepassing is binnen enkele ogenblikken gemaakt en geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-168">Your application builds and deploys within a few moments.</span></span> <span data-ttu-id="d9eaf-169">U kunt de implementatiestatus Hallo in Service Fabric Explorer bewaken.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-169">You can monitor hello deployment status in Service Fabric Explorer.</span></span>  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a><span data-ttu-id="d9eaf-170">Een Service Fabric-service tooyour Service Fabric-toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="d9eaf-170">Add a Service Fabric service tooyour Service Fabric application</span></span>

<span data-ttu-id="d9eaf-171">een Service Fabric-service tooan bestaande Service Fabric-toepassing, tooadd Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-171">tooadd a Service Fabric service tooan existing Service Fabric application, do hello following steps:</span></span>

1.  <span data-ttu-id="d9eaf-172">Met de rechtermuisknop op Hallo-project dat u wilt dat een service tooadd en klik vervolgens op **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-172">Right-click hello project you want tooadd a service to, and then click **Service Fabric**.</span></span>

    ![Service aan Service Fabric toevoegen pagina 1][add-service/p1]

2.  <span data-ttu-id="d9eaf-174">Klik op **Service Fabric-Service toevoegen**, en volledige Hallo set stappen tooadd een toohello serviceproject.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-174">Click **Add Service Fabric Service**, and complete hello set of steps tooadd a service toohello project.</span></span>
3.  <span data-ttu-id="d9eaf-175">Selecteer Hallo servicesjabloon u wilt tooadd tooyour project en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-175">Select hello service template you want tooadd tooyour project, and then click **Next**.</span></span>

    ![Service aan Service Fabric toevoegen pagina 2][add-service/p2]

4.  <span data-ttu-id="d9eaf-177">Voer de naam van de service Hallo (en andere details, indien nodig) en klik vervolgens op Hallo **Service toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-177">Enter hello service name (and other details, as needed), and then click hello **Add Service** button.</span></span>  

    ![Service aan Service Fabric toevoegen pagina 3][add-service/p3]

5.  <span data-ttu-id="d9eaf-179">Nadat Hallo-service wordt toegevoegd, zoekt de projectstructuur van uw algehele vergelijkbare toohello project te volgen:</span><span class="sxs-lookup"><span data-stu-id="d9eaf-179">After hello service is added, your overall project structure looks similar toohello following project:</span></span>

    ![Service aan Service Fabric toevoegen pagina 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a><span data-ttu-id="d9eaf-181">Manifestversies van uw Service Fabric Java-toepassing bewerken</span><span class="sxs-lookup"><span data-stu-id="d9eaf-181">Edit Manifest versions of your Service Fabric Java application</span></span>

<span data-ttu-id="d9eaf-182">tooedit manifest versies, klik met de rechtermuisknop op het Hallo-project, gaat u te**Service Fabric** en selecteer **Manifest versies bewerken...**  van Hallo vervolgmenu.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-182">tooedit manifest versions, right click on hello project, go too**Service Fabric** and select **Edit Manifest Versions...** from hello menu dropdown.</span></span> <span data-ttu-id="d9eaf-183">In de wizard hello, kunt u manifest versies voor het manifest, servicemanifest toepassing hello en Hallo voor bijwerken **Code**, **Config** en **gegevens** pakketten.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-183">In hello wizard, you can update hello manifest versions for application manifest, service manifest and hello versions for **Code**, **Config** and **Data** packages.</span></span>

<span data-ttu-id="d9eaf-184">Als u het selectievakje Hallo optie **automatisch bijwerken van toepassing en Serviceversies** en werk vervolgens een versie, Hallo manifest versies vervolgens automatisch bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-184">If you check hello option **Automatically update application and service versions** and then update a version, then hello manifest versions will be automatically updated.</span></span> <span data-ttu-id="d9eaf-185">toogive bijvoorbeeld u eerst Kies selectievakje Hallo Hallo updateversie van **Code** -versie uit 0.0.0 too0.0.1 en klik op **voltooien**, klikt u vervolgens service manifest versie en het toepassingsmanifest versie wordt automatisch bijgewerkt too0.0.1 zijn.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-185">toogive an example, you first select hello check-box, then update hello version of **Code** version from 0.0.0 too0.0.1 and click on **Finish**, then service manifest version and application manifest version will be automatically updated too0.0.1.</span></span>

## <a name="upgrade-your-service-fabric-java-application"></a><span data-ttu-id="d9eaf-186">Uw Service Fabric Java-toepassing upgraden</span><span class="sxs-lookup"><span data-stu-id="d9eaf-186">Upgrade your Service Fabric Java application</span></span>

<span data-ttu-id="d9eaf-187">Voor een upgradescenario aannemen dat u hebt gemaakt Hallo **App1** project met behulp van Hallo Service Fabric-invoegtoepassing in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-187">For an upgrade scenario, say you created hello **App1** project by using hello Service Fabric plug-in in Eclipse.</span></span> <span data-ttu-id="d9eaf-188">Hebt geïmplementeerd met behulp van de invoegtoepassing toocreate Hallo een toepassing met de naam **fabric: / App1Application**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-188">You deployed it by using hello plug-in toocreate an application named **fabric:/App1Application**.</span></span> <span data-ttu-id="d9eaf-189">Hallo toepassingstype **App1AppicationType**, en versie van de toepassing hello 1.0 is.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-189">hello application type is **App1AppicationType**, and hello application version is 1.0.</span></span> <span data-ttu-id="d9eaf-190">Nu u tooupgrade uw toepassing zonder de beschikbaarheid te onderbreken.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-190">Now, you want tooupgrade your application without interrupting availability.</span></span>

<span data-ttu-id="d9eaf-191">Controleer eerst eventuele wijzigingen tooyour toepassing en vervolgens opnieuw opbouwen Hallo service gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-191">First, make any changes tooyour application, and then rebuild hello modified service.</span></span> <span data-ttu-id="d9eaf-192">Hallo update gewijzigd van service manifestbestand (ServiceManifest.xml) met de Hallo bijgewerkt versies voor het Hallo-service (en, Config of gegevens, zoals relevante).</span><span class="sxs-lookup"><span data-stu-id="d9eaf-192">Update hello modified service’s manifest file (ServiceManifest.xml) with hello updated versions for hello service (and Code, Config, or Data, as relevant).</span></span> <span data-ttu-id="d9eaf-193">Ook wijzigen van de toepassing hello-manifest (ApplicationManifest.xml) met versienummer Hallo bijgewerkt voor de toepassing hello en Hallo gewijzigde service.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-193">Also, modify hello application’s manifest (ApplicationManifest.xml) with hello updated version number for hello application and hello modified service.</span></span>  

<span data-ttu-id="d9eaf-194">tooupgrade uw toepassing met behulp van Eclipse Neon, kunt u een dubbele uitvoeren configuratieprofiel.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-194">tooupgrade your application by using Eclipse Neon, you can create a duplicate run configuration profile.</span></span> <span data-ttu-id="d9eaf-195">Gebruik vervolgens tooupgrade uw toepassing naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-195">Then, use it tooupgrade your application as needed.</span></span>

1.  <span data-ttu-id="d9eaf-196">Ga te**uitvoeren** > **configuratie uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-196">Go too**Run** > **Run Configurations**.</span></span> <span data-ttu-id="d9eaf-197">Klik in het linkerdeelvenster Hallo Hallo pijltje toohello links van **Project met Gradle**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-197">In hello left pane, click hello small arrow toohello left of **Gradle Project**.</span></span>
2.  <span data-ttu-id="d9eaf-198">Klik met de rechtermuisknop op **ServiceFabricDeployer** en selecteer **Duplicate**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-198">Right-click **ServiceFabricDeployer**, and then select **Duplicate**.</span></span> <span data-ttu-id="d9eaf-199">Voer een nieuwe naam in voor deze configuratie, bijvoorbeeld **ServiceFabricUpgrader**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-199">Enter a new name for this configuration, for example, **ServiceFabricUpgrader**.</span></span>
3.  <span data-ttu-id="d9eaf-200">In het rechterpaneel Hallo op Hallo **argumenten** en wijzig **- Pconfig = 'implementeren'** te**- Pconfig = 'bijwerken'**, en klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-200">In hello right panel, on hello **Arguments** tab, change **-Pconfig='deploy'** too**-Pconfig='upgrade'**, and then click **Apply**.</span></span>

<span data-ttu-id="d9eaf-201">Dit proces wordt gemaakt en opgeslagen configuratieprofiel uitvoeren u kunt gebruiken om uw toepassing op alle tooupgrade tijd.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-201">This process creates and saves a run configuration profile you can use at any time tooupgrade your application.</span></span> <span data-ttu-id="d9eaf-202">Ook krijgt Hallo meest recente bijgewerkte versie van het toepassingstype van manifestbestand van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-202">It also gets hello latest updated application type version from hello application manifest file.</span></span>

<span data-ttu-id="d9eaf-203">upgrade van de toepassing Hello duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-203">hello application upgrade takes a few minutes.</span></span> <span data-ttu-id="d9eaf-204">U kunt de upgrade van de toepassing hello in Service Fabric Explorer bewaken.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-204">You can monitor hello application upgrade in Service Fabric Explorer.</span></span>

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="d9eaf-205">Oude Service Fabric-Java-toepassingen toobe gebruikt met Maven migreren</span><span class="sxs-lookup"><span data-stu-id="d9eaf-205">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="d9eaf-206">We hebben onlangs Service Fabric-Java-bibliotheken verplaatst vanuit Service Fabric Java SDK tooMaven opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-206">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="d9eaf-207">Tijdens het Hallo nieuwe toepassingen die u met behulp van Eclipse genereren genereert de meest recente bijgewerkte projecten (die worden kunnen toowork met Maven), kunt u uw bestaande Service Fabric staatloze of actor Java-toepassingen, wat Hallo Service Fabric Java SDK gebruikten bijwerken eerdere versies, toouse Hallo Service Fabric Java afhankelijkheden van Maven.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-207">While hello new applications you generate using Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="d9eaf-208">Stappen Hallo vermeld [hier](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure de oudere toepassing met Maven werkt.</span><span class="sxs-lookup"><span data-stu-id="d9eaf-208">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

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
