---
title: aaaHow toouse hello Azure slave invoegtoepassing met Hudson continue integratie | Microsoft Docs
description: Hierin wordt beschreven hoe toouse hello Azure slave invoegtoepassing met Hudson continue integratie.
services: virtual-machines-linux
documentationcenter: 
author: rmcmurray
manager: wpickett
editor: 
ms.assetid: b2083d1c-4de8-4a19-a615-ccc9d9b6e1d9
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cd6e67ad71c208aa56746aa8b70ba507da20bee9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="73b7b-103">Hoe toouse hello Azure slave invoegtoepassing met Hudson continue integratie</span><span class="sxs-lookup"><span data-stu-id="73b7b-103">How toouse hello Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="73b7b-104">Hello Azure slave invoegtoepassing voor Hudson kunt u tooprovision slave knooppunten op Azure bij het uitvoeren van gedistribueerde bouwt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-104">hello Azure slave plug-in for Hudson enables you tooprovision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-hello-azure-slave-plug-in"></a><span data-ttu-id="73b7b-105">Hello Azure Slave invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="73b7b-105">Install hello Azure Slave plug-in</span></span>
1. <span data-ttu-id="73b7b-106">In Hallo Hudson dashboard, klikt u op **Hudson beheren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-106">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="73b7b-107">In Hallo **beheren Hudson** pagina, klikt u op **invoegtoepassingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-107">In hello **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="73b7b-108">Klik op Hallo **beschikbaar** tabblad.</span><span class="sxs-lookup"><span data-stu-id="73b7b-108">Click hello **Available** tab.</span></span>
4. <span data-ttu-id="73b7b-109">Klik op **Search** en het type **Azure** toolimit Hallo lijst toorelevant invoegtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="73b7b-109">Click **Search** and type **Azure** toolimit hello list toorelevant plug-ins.</span></span>
   
    <span data-ttu-id="73b7b-110">Als u ervoor tooscroll door Hallo lijst met beschikbare invoegtoepassingen kiezen, vindt u hello Azure slave invoegtoepassing onder Hallo **Clusterbeheer en gedistribueerd bouwen** sectie in Hallo **anderen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="73b7b-110">If you opt tooscroll through hello list of available plug-ins, you will find hello Azure slave plug-in under hello **Cluster Management and Distributed Build** section in hello **Others** tab.</span></span>
5. <span data-ttu-id="73b7b-111">Schakel dit selectievakje in Hallo voor **Azure Slave invoegtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-111">Select hello checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="73b7b-112">Klik op **Install**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-112">Click **Install**.</span></span>
7. <span data-ttu-id="73b7b-113">Opnieuw opstarten Hudson.</span><span class="sxs-lookup"><span data-stu-id="73b7b-113">Restart Hudson.</span></span>

<span data-ttu-id="73b7b-114">Nu die Hallo invoegtoepassing is geïnstalleerd, zou de volgende stappen Hallo tooconfigure Hallo invoegtoepassing met uw Azure-abonnement profiel en een sjabloon die wordt gebruikt bij het maken van Hallo VM voor Hallo slave knooppunt toocreate zijn.</span><span class="sxs-lookup"><span data-stu-id="73b7b-114">Now that hello plug-in is installed, hello next steps would be tooconfigure hello plug-in with your Azure subscription profile and toocreate a template that will be used in creating hello VM for hello slave node.</span></span>

## <a name="configure-hello-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="73b7b-115">Hello Azure Slave invoegtoepassing configureren met het profiel van uw abonnement</span><span class="sxs-lookup"><span data-stu-id="73b7b-115">Configure hello Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="73b7b-116">Een profiel abonnement ook waarnaar wordt verwezen tooas publicatie-instellingen, is een XML-bestand met beveiligde referenties en aanvullende informatie moet u toowork met Azure in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="73b7b-116">A subscription profile, also referred tooas publish settings, is an XML file that contains secure credentials and some additional information you'll need toowork with Azure in your development environment.</span></span> <span data-ttu-id="73b7b-117">tooconfigure hello Azure slave invoegtoepassing, moet u de:</span><span class="sxs-lookup"><span data-stu-id="73b7b-117">tooconfigure hello Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="73b7b-118">Uw abonnements-id</span><span class="sxs-lookup"><span data-stu-id="73b7b-118">Your subscription id</span></span>
* <span data-ttu-id="73b7b-119">Een beheercertificaat voor uw abonnement</span><span class="sxs-lookup"><span data-stu-id="73b7b-119">A management certificate for your subscription</span></span>

<span data-ttu-id="73b7b-120">Deze vindt u in uw [abonnement profiel].</span><span class="sxs-lookup"><span data-stu-id="73b7b-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="73b7b-121">Hieronder volgt een voorbeeld van een profiel voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="73b7b-121">Below is an example of a subscription profile.</span></span>

    <?xml version="1.0" encoding="utf-8"?>

        <PublishData>

          <PublishProfile SchemaVersion="2.0" PublishMethod="AzureServiceManagementAPI">

        <Subscription

              ServiceManagementUrl="https://management.core.windows.net"

              Id="<Subscription ID>"

              Name="Pay-As-You-Go"
            ManagementCertificate="<Management certificate value>" />

          </PublishProfile>

    </PublishData>

<span data-ttu-id="73b7b-122">Zodra u het profiel van uw abonnement hebt, volgt u deze stappen tooconfigure hello Azure slave invoegtoepassing.</span><span class="sxs-lookup"><span data-stu-id="73b7b-122">Once you have your subscription profile, follow these steps tooconfigure hello Azure slave plug-in.</span></span>

1. <span data-ttu-id="73b7b-123">In Hallo Hudson dashboard, klikt u op **Hudson beheren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-123">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="73b7b-124">Klik op **systeem configureren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="73b7b-125">Schuif omlaag Hallo pagina toofind hello **Cloud** sectie.</span><span class="sxs-lookup"><span data-stu-id="73b7b-125">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="73b7b-126">Klik op **toevoegen van nieuwe cloud > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![toevoegen van nieuwe cloud][add new cloud]
   
    <span data-ttu-id="73b7b-128">Hier ziet uw abonnementsgegevens Hallo velden waar u tooenter nodig.</span><span class="sxs-lookup"><span data-stu-id="73b7b-128">This will show hello fields where you need tooenter your subscription details.</span></span>
   
    ![profiel configureren][configure profile]
5. <span data-ttu-id="73b7b-130">Kopiëren Hallo abonnements-id en het beheer van het certificaat uit het profiel van uw abonnement en plak deze in de juiste velden Hallo.</span><span class="sxs-lookup"><span data-stu-id="73b7b-130">Copy hello subscription id and management certificate from your subscription profile and paste them in hello appropriate fields.</span></span>
   
    <span data-ttu-id="73b7b-131">Bij het kopiëren van Hallo abonnement-id en het beheer certificaat **niet** Hallo aanhalingstekens die Hallo-waarden insluiten bevatten.</span><span class="sxs-lookup"><span data-stu-id="73b7b-131">When copying hello subscription id and management certificate, **do not** include hello quotes that enclose hello values.</span></span>
6. <span data-ttu-id="73b7b-132">Klik op **controleren configuratie**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="73b7b-133">Wanneer het Hallo-configuratie is geverifieerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-133">When hello configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-hello-azure-slave-plug-in"></a><span data-ttu-id="73b7b-134">Een virtuele machine-sjabloon voor hello Azure Slave invoegtoepassing instellen</span><span class="sxs-lookup"><span data-stu-id="73b7b-134">Set up a virtual machine template for hello Azure Slave plug-in</span></span>
<span data-ttu-id="73b7b-135">Een sjabloon voor virtuele machines Hallo parameters definieert Hallo invoegtoepassing gebruikt toocreate een knooppunt slave op Azure.</span><span class="sxs-lookup"><span data-stu-id="73b7b-135">A virtual machine template defines hello parameters hello plug-in will use toocreate a slave node on Azure.</span></span> <span data-ttu-id="73b7b-136">In de volgende stappen uit Hallo maakt we sjabloon voor een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="73b7b-136">In hello following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="73b7b-137">In Hallo Hudson dashboard, klikt u op **Hudson beheren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-137">In hello Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="73b7b-138">Klik op **systeem configureren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="73b7b-139">Schuif omlaag Hallo pagina toofind hello **Cloud** sectie.</span><span class="sxs-lookup"><span data-stu-id="73b7b-139">Scroll down hello page toofind hello **Cloud** section.</span></span>
4. <span data-ttu-id="73b7b-140">Binnen Hallo **Cloud** sectie, zoeken **Azure virtuele Machine-sjabloon toevoegen** en klik op Hallo **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="73b7b-140">Within hello **Cloud** section, find **Add Azure Virtual Machine Template** and click hello **Add** button.</span></span>
   
    ![vm-sjabloon toevoegen][add vm template]
5. <span data-ttu-id="73b7b-142">Geef de naam van een cloudservice in Hallo **naam** veld.</span><span class="sxs-lookup"><span data-stu-id="73b7b-142">Specify a cloud service name in hello **Name** field.</span></span> <span data-ttu-id="73b7b-143">Als Hallo-naam die u opgeeft tooan bestaande cloudservice verwijst, worden Hallo VM ingericht in die service.</span><span class="sxs-lookup"><span data-stu-id="73b7b-143">If hello name you specify refers tooan existing cloud service, hello VM will be provisioned in that service.</span></span> <span data-ttu-id="73b7b-144">Azure wordt anders maakt u een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="73b7b-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="73b7b-145">In Hallo **beschrijving** en voer de tekst die beschrijft Hallo-sjabloon die u maakt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-145">In hello **Description** field, enter text that describes hello template you are creating.</span></span> <span data-ttu-id="73b7b-146">Deze informatie wordt alleen gebruikt voor administratieve doeleinden en wordt niet gebruikt in een VM-inrichting.</span><span class="sxs-lookup"><span data-stu-id="73b7b-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="73b7b-147">In Hallo **Labels** veld **linux**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-147">In hello **Labels** field, enter **linux**.</span></span> <span data-ttu-id="73b7b-148">Dit label is gebruikte tooidentify Hallo sjabloon die u maakt en vervolgens gebruikte tooreference Hallo sjabloon bij het maken van een taak Hudson.</span><span class="sxs-lookup"><span data-stu-id="73b7b-148">This label is used tooidentify hello template you are creating and is subsequently used tooreference hello template when creating a Hudson job.</span></span>
8. <span data-ttu-id="73b7b-149">Selecteer een regio waar Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-149">Select a region where hello VM will be created.</span></span>
9. <span data-ttu-id="73b7b-150">Selecteer de relevante VM-grootte Hallo.</span><span class="sxs-lookup"><span data-stu-id="73b7b-150">Select hello appropriate VM size.</span></span>
10. <span data-ttu-id="73b7b-151">Geef een opslagaccount waar Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-151">Specify a storage account where hello VM will be created.</span></span> <span data-ttu-id="73b7b-152">Zorg ervoor dat deze zich in Hallo dezelfde regio als Hallo cloudservice die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="73b7b-152">Make sure that it is in hello same region as hello cloud service you'll be using.</span></span> <span data-ttu-id="73b7b-153">Als u nieuwe opslag toobe gemaakt wilt, kunt u dit veld leeg laten.</span><span class="sxs-lookup"><span data-stu-id="73b7b-153">If you want new storage toobe created, you can leave this field blank.</span></span>
11. <span data-ttu-id="73b7b-154">Bewaartijd geeft het aantal minuten op voordat Hudson wordt verwijderd als een niet-actieve slave Hallo.</span><span class="sxs-lookup"><span data-stu-id="73b7b-154">Retention time specifies hello number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="73b7b-155">Dit laat de standaardwaarde Hallo van 60.</span><span class="sxs-lookup"><span data-stu-id="73b7b-155">Leave this at hello default value of 60.</span></span>
12. <span data-ttu-id="73b7b-156">In **gebruik**, selecteer welke voorwaarde Hallo wanneer dit knooppunt slave wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-156">In **Usage**, select hello appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="73b7b-157">Selecteer nu **gebruikmaken van dit knooppunt zo veel mogelijk**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="73b7b-158">Op dit moment eruit uw formulier enigszins vergelijkbaar toothis:</span><span class="sxs-lookup"><span data-stu-id="73b7b-158">At this point, your form would look somewhat similar toothis:</span></span>
    
     ![De sjabloonconfiguratie][template config]
13. <span data-ttu-id="73b7b-160">In **installatiekopie familie-Id of** hebt toospecify welke installatiekopie wordt geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="73b7b-160">In **Image Family or Id** you have toospecify what system image will be installed on your VM.</span></span> <span data-ttu-id="73b7b-161">U kunt selecteren in een lijst van families van de afbeelding of geef een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="73b7b-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="73b7b-162">Als u tooselect uit een lijst met installatiekopie families wilt, Voer Hallo eerste teken (hoofdlettergevoelig) van familienaam Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="73b7b-162">If you want tooselect from a list of image families, enter hello first character (case-sensitive) of hello image family name.</span></span> <span data-ttu-id="73b7b-163">Voor het exemplaar typen **U** verschijnt nu een lijst met Ubuntu Server families.</span><span class="sxs-lookup"><span data-stu-id="73b7b-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="73b7b-164">Wanneer u in de lijst hello selecteert, Jenkins Hallo meest recente versie van deze installatiekopie van die familie gebruikt bij het inrichten van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="73b7b-164">Once you select from hello list, Jenkins will use hello latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![Lijst met familie van besturingssystemen][OS family list]
    
     <span data-ttu-id="73b7b-166">Als u een aangepaste installatiekopie dat u wilt dat toouse in plaats daarvan hebt, Voer Hallo-naam van de aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="73b7b-166">If you have a custom image that you want toouse instead, enter hello name of that custom image.</span></span> <span data-ttu-id="73b7b-167">Afbeelding van aangepaste namen worden niet weergegeven in een lijst zodat u tooensure die Hallo naam correct is ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="73b7b-167">Custom image names are not shown in a list so you have tooensure that hello name is entered correctly.</span></span>    
    
     <span data-ttu-id="73b7b-168">Typ voor deze zelfstudie **U** toobring een lijst weergegeven van Ubuntu-installatiekopieën en selecteer **Ubuntu Server 14.04 TNS**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-168">For this tutorial, type **U** toobring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="73b7b-169">Voor **methode starten**, selecteer **SSH**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="73b7b-170">Hallo onderstaande script kopiëren en plakken op Hallo **Init script** veld.</span><span class="sxs-lookup"><span data-stu-id="73b7b-170">Copy hello script below and paste in hello **Init script** field.</span></span>
    
         # Install Java
    
         sudo apt-get -y update
    
         sudo apt-get install -y openjdk-7-jdk
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y openjdk-7-jdk
    
         # Install git
    
         sudo apt-get install -y git
    
         #Install ant
    
         sudo apt-get install -y ant
    
         sudo apt-get -y update --fix-missing
    
         sudo apt-get install -y ant
    
     <span data-ttu-id="73b7b-171">Hallo **Init script** worden uitgevoerd na Hallo virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-171">hello **Init script** will be executed after hello VM is created.</span></span> <span data-ttu-id="73b7b-172">In dit voorbeeld installeert Hallo script Java, git en ant.</span><span class="sxs-lookup"><span data-stu-id="73b7b-172">In this example, hello script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="73b7b-173">In Hallo **gebruikersnaam** en **wachtwoord** velden, voert u de gewenste waarden voor Hallo administrator-account dat wordt gemaakt op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="73b7b-173">In hello **Username** and **Password** fields, enter your preferred values for hello administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="73b7b-174">Klik op **sjabloon controleren** toocheck als Hallo-parameters die u hebt opgegeven geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="73b7b-174">Click on **Verify Template** toocheck if hello parameters you specified are valid.</span></span>
18. <span data-ttu-id="73b7b-175">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="73b7b-176">Een taak Hudson die wordt uitgevoerd op een lager niveau bevindende-knooppunt in Azure maken</span><span class="sxs-lookup"><span data-stu-id="73b7b-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="73b7b-177">In deze sectie maakt u een Hudson-taak die wordt uitgevoerd op een knooppunt slave op Azure.</span><span class="sxs-lookup"><span data-stu-id="73b7b-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="73b7b-178">In Hallo Hudson dashboard, klikt u op **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-178">In hello Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="73b7b-179">Voer een naam voor de Hallo-taak die u maakt.</span><span class="sxs-lookup"><span data-stu-id="73b7b-179">Enter a name for hello job you are creating.</span></span>
3. <span data-ttu-id="73b7b-180">Selecteer Hallo taaktype **bouwen van een taak vrije-stijl software**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-180">For hello job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="73b7b-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-181">Click **OK**.</span></span>
5. <span data-ttu-id="73b7b-182">Selecteer in de taak configuratiepagina Hallo **beperken waar dit project kan worden uitgevoerd**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-182">In hello job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="73b7b-183">Selecteer **knooppunt en label menu** en selecteer **linux** (we opgegeven dit label bij het maken van virtuele-machinesjabloon Hallo in de vorige sectie Hallo).</span><span class="sxs-lookup"><span data-stu-id="73b7b-183">Select **Node and label menu** and select **linux** (we specified this label when creating hello virtual machine template in hello previous section).</span></span>
7. <span data-ttu-id="73b7b-184">In Hallo **bouwen** sectie, klikt u op **toevoegen build stap** en selecteer **shell uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-184">In hello **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="73b7b-185">Hallo script volgen en vervangt bewerken **{uw github-accountnaam}**, **{projectnaam van uw}**, en **{uw projectmap}** met waarden nodig en Hallo plakken bewerkt script Hallo tekst in die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="73b7b-185">Edit hello following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste hello edited script in hello text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory tooproject
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="73b7b-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="73b7b-186">Click on **Save**.</span></span>
10. <span data-ttu-id="73b7b-187">In Hallo Hudson dashboard, zoek de Hallo-taak die u zojuist hebt gemaakt en klik op Hallo **plannen van een build** pictogram.</span><span class="sxs-lookup"><span data-stu-id="73b7b-187">In hello Hudson dashboard, find hello job you just created and click on hello **Schedule a build** icon.</span></span>

<span data-ttu-id="73b7b-188">Hudson vervolgens maakt u een lager niveau bevindende knooppunt met Hallo-sjabloon is gemaakt in de vorige sectie Hallo en Hallo-script die u hebt opgegeven in Hallo build stap voor deze taak uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="73b7b-188">Hudson will then create a slave node using hello template created in hello previous section and execute hello script you specified in hello build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73b7b-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73b7b-189">Next Steps</span></span>
<span data-ttu-id="73b7b-190">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="73b7b-190">For more information about using Azure with Java, see hello [Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[abonnement profiel]: http://go.microsoft.com/fwlink/?LinkID=396395

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

