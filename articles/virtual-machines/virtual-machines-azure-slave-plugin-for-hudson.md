---
title: Het gebruik van de invoegtoepassing Azure slave met Hudson continue integratie | Microsoft Docs
description: Beschrijft hoe u de invoegtoepassing Azure slave met Hudson continue integratie.
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
ms.openlocfilehash: c11b59f8ea432075b147a391de4b7bd3331e639e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-azure-slave-plug-in-with-hudson-continuous-integration"></a><span data-ttu-id="bfd3d-103">Het gebruik van de invoegtoepassing Azure slave met Hudson continue integratie</span><span class="sxs-lookup"><span data-stu-id="bfd3d-103">How to use the Azure slave plug-in with Hudson Continuous Integration</span></span>
<span data-ttu-id="bfd3d-104">De invoegtoepassing voor Hudson Azure slave kunt u knooppunten van de slave op Azure inrichten bij het uitvoeren van gedistribueerde bouwt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-104">The Azure slave plug-in for Hudson enables you to provision slave nodes on Azure when running distributed builds.</span></span>

## <a name="install-the-azure-slave-plug-in"></a><span data-ttu-id="bfd3d-105">De Azure-Slave invoegtoepassing installeren</span><span class="sxs-lookup"><span data-stu-id="bfd3d-105">Install the Azure Slave plug-in</span></span>
1. <span data-ttu-id="bfd3d-106">Klik in het dashboard Hudson **Hudson beheren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-106">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="bfd3d-107">In de **beheren Hudson** pagina, klikt u op **invoegtoepassingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-107">In the **Manage Hudson** page, click on **Manage Plugins**.</span></span>
3. <span data-ttu-id="bfd3d-108">Klik op de **beschikbaar** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-108">Click the **Available** tab.</span></span>
4. <span data-ttu-id="bfd3d-109">Klik op **Search** en het type **Azure** te beperken van de lijst om de relevante invoegtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-109">Click **Search** and type **Azure** to limit the list to relevant plug-ins.</span></span>
   
    <span data-ttu-id="bfd3d-110">Als u ervoor kiezen om te bladeren door de lijst met beschikbare invoegtoepassingen, vindt u de Azure slave invoegtoepassing onder de **Clusterbeheer en gedistribueerd bouwen** sectie het **anderen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-110">If you opt to scroll through the list of available plug-ins, you will find the Azure slave plug-in under the **Cluster Management and Distributed Build** section in the **Others** tab.</span></span>
5. <span data-ttu-id="bfd3d-111">Schakel het selectievakje voor **Azure Slave invoegtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-111">Select the checkbox for **Azure Slave Plugin**.</span></span>
6. <span data-ttu-id="bfd3d-112">Klik op **Install**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-112">Click **Install**.</span></span>
7. <span data-ttu-id="bfd3d-113">Opnieuw opstarten Hudson.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-113">Restart Hudson.</span></span>

<span data-ttu-id="bfd3d-114">Nu dat de invoegtoepassing is geïnstalleerd, worden de volgende stappen voor het configureren van de invoegtoepassing met het profiel van uw Azure-abonnement en een sjabloon die wordt gebruikt bij het maken van de virtuele machine voor het knooppunt slave maken.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-114">Now that the plug-in is installed, the next steps would be to configure the plug-in with your Azure subscription profile and to create a template that will be used in creating the VM for the slave node.</span></span>

## <a name="configure-the-azure-slave-plug-in-with-your-subscription-profile"></a><span data-ttu-id="bfd3d-115">De Azure-Slave invoegtoepassing configureren met het profiel van uw abonnement</span><span class="sxs-lookup"><span data-stu-id="bfd3d-115">Configure the Azure Slave plug-in with your subscription profile</span></span>
<span data-ttu-id="bfd3d-116">Een abonnement-profiel, ook bekend als de publicatie-instellingen, is een XML-bestand met beveiligde referenties en wat extra informatie die u wilt werken met Azure in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-116">A subscription profile, also referred to as publish settings, is an XML file that contains secure credentials and some additional information you'll need to work with Azure in your development environment.</span></span> <span data-ttu-id="bfd3d-117">Voor het configureren van de invoegtoepassing Azure slave, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="bfd3d-117">To configure the Azure slave plug-in, you need:</span></span>

* <span data-ttu-id="bfd3d-118">Uw abonnements-id</span><span class="sxs-lookup"><span data-stu-id="bfd3d-118">Your subscription id</span></span>
* <span data-ttu-id="bfd3d-119">Een beheercertificaat voor uw abonnement</span><span class="sxs-lookup"><span data-stu-id="bfd3d-119">A management certificate for your subscription</span></span>

<span data-ttu-id="bfd3d-120">Deze vindt u in uw [abonnement profiel].</span><span class="sxs-lookup"><span data-stu-id="bfd3d-120">These can be found in your [subscription profile].</span></span> <span data-ttu-id="bfd3d-121">Hieronder volgt een voorbeeld van een profiel voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-121">Below is an example of a subscription profile.</span></span>

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

<span data-ttu-id="bfd3d-122">Zodra u het profiel van uw abonnement hebt, volg deze stappen voor het configureren van de invoegtoepassing Azure slave.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-122">Once you have your subscription profile, follow these steps to configure the Azure slave plug-in.</span></span>

1. <span data-ttu-id="bfd3d-123">Klik in het dashboard Hudson **Hudson beheren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-123">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="bfd3d-124">Klik op **systeem configureren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-124">Click **Configure System**.</span></span>
3. <span data-ttu-id="bfd3d-125">Schuif omlaag in de pagina naar de **Cloud** sectie.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-125">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="bfd3d-126">Klik op **toevoegen van nieuwe cloud > Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-126">Click **Add new cloud > Microsoft Azure**.</span></span>
   
    ![toevoegen van nieuwe cloud][add new cloud]
   
    <span data-ttu-id="bfd3d-128">Hier ziet de velden waarop u moet uw abonnementsgegevens invoeren.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-128">This will show the fields where you need to enter your subscription details.</span></span>
   
    ![profiel configureren][configure profile]
5. <span data-ttu-id="bfd3d-130">Het abonnement-id en het beheer certificaat uit het profiel van uw abonnement Kopieer en plak deze in de juiste velden.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-130">Copy the subscription id and management certificate from your subscription profile and paste them in the appropriate fields.</span></span>
   
    <span data-ttu-id="bfd3d-131">Bij het kopiëren van het abonnement-id en de management-certificaat **niet** de aanhalingstekens die plaatst u de waarden.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-131">When copying the subscription id and management certificate, **do not** include the quotes that enclose the values.</span></span>
6. <span data-ttu-id="bfd3d-132">Klik op **controleren configuratie**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-132">Click on **Verify configuration**.</span></span>
7. <span data-ttu-id="bfd3d-133">Wanneer de configuratie is geverifieerd, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-133">When the configuration is verified successfully, click **Save**.</span></span>

## <a name="set-up-a-virtual-machine-template-for-the-azure-slave-plug-in"></a><span data-ttu-id="bfd3d-134">Een virtuele machine-sjabloon instellen voor de Azure-Slave invoegtoepassing</span><span class="sxs-lookup"><span data-stu-id="bfd3d-134">Set up a virtual machine template for the Azure Slave plug-in</span></span>
<span data-ttu-id="bfd3d-135">Een VM-sjabloon definieert de parameters die de invoegtoepassing wordt gebruikt voor het maken van een knooppunt slave op Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-135">A virtual machine template defines the parameters the plug-in will use to create a slave node on Azure.</span></span> <span data-ttu-id="bfd3d-136">In de volgende stappen maakt we sjabloon voor een Ubuntu VM.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-136">In the following steps we'll be creating template for an Ubuntu VM.</span></span>

1. <span data-ttu-id="bfd3d-137">Klik in het dashboard Hudson **Hudson beheren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-137">In the Hudson dashboard, click **Manage Hudson**.</span></span>
2. <span data-ttu-id="bfd3d-138">Klik op **systeem configureren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-138">Click on **Configure System**.</span></span>
3. <span data-ttu-id="bfd3d-139">Schuif omlaag in de pagina naar de **Cloud** sectie.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-139">Scroll down the page to find the **Cloud** section.</span></span>
4. <span data-ttu-id="bfd3d-140">Binnen de **Cloud** sectie, zoeken **Azure virtuele Machine-sjabloon toevoegen** en klik op de **toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-140">Within the **Cloud** section, find **Add Azure Virtual Machine Template** and click the **Add** button.</span></span>
   
    ![vm-sjabloon toevoegen][add vm template]
5. <span data-ttu-id="bfd3d-142">Geef de naam van een cloudservice in de **naam** veld.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-142">Specify a cloud service name in the **Name** field.</span></span> <span data-ttu-id="bfd3d-143">Als de opgegeven naam naar een bestaande cloudservice verwijst, dat de virtuele machine wordt ingericht in die service.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-143">If the name you specify refers to an existing cloud service, the VM will be provisioned in that service.</span></span> <span data-ttu-id="bfd3d-144">Azure wordt anders maakt u een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-144">Otherwise, Azure will create a new one.</span></span>
6. <span data-ttu-id="bfd3d-145">In de **beschrijving** en voer de tekst die beschrijft de sjabloon die u maakt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-145">In the **Description** field, enter text that describes the template you are creating.</span></span> <span data-ttu-id="bfd3d-146">Deze informatie wordt alleen gebruikt voor administratieve doeleinden en wordt niet gebruikt in een VM-inrichting.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-146">This information is only for documentary purposes and is not used in provisioning a VM.</span></span>
7. <span data-ttu-id="bfd3d-147">In de **Labels** veld **linux**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-147">In the **Labels** field, enter **linux**.</span></span> <span data-ttu-id="bfd3d-148">Dit label wordt gebruikt voor het identificeren van de sjabloon die u maakt en vervolgens worden gebruikt om te verwijzen naar de sjabloon bij het maken van een taak Hudson.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-148">This label is used to identify the template you are creating and is subsequently used to reference the template when creating a Hudson job.</span></span>
8. <span data-ttu-id="bfd3d-149">Selecteer een regio waar de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-149">Select a region where the VM will be created.</span></span>
9. <span data-ttu-id="bfd3d-150">Selecteer de relevante VM-grootte.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-150">Select the appropriate VM size.</span></span>
10. <span data-ttu-id="bfd3d-151">Geef een opslagaccount waar de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-151">Specify a storage account where the VM will be created.</span></span> <span data-ttu-id="bfd3d-152">Zorg ervoor dat deze zich in dezelfde regio bevinden als de cloudservice die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-152">Make sure that it is in the same region as the cloud service you'll be using.</span></span> <span data-ttu-id="bfd3d-153">Als u wilt dat nieuwe opslag worden gemaakt, kunt u dit veld leeg laten.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-153">If you want new storage to be created, you can leave this field blank.</span></span>
11. <span data-ttu-id="bfd3d-154">Bewaartijd geeft het aantal minuten voordat Hudson wordt een niet-actieve slave verwijderd.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-154">Retention time specifies the number of minutes before Hudson deletes an idle slave.</span></span> <span data-ttu-id="bfd3d-155">Dit laat de standaardwaarde van 60.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-155">Leave this at the default value of 60.</span></span>
12. <span data-ttu-id="bfd3d-156">In **gebruik**, selecteert u de juiste voorwaarde wanneer dit knooppunt slave wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-156">In **Usage**, select the appropriate condition when this slave node will be used.</span></span> <span data-ttu-id="bfd3d-157">Selecteer nu **gebruikmaken van dit knooppunt zo veel mogelijk**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-157">For now, select **Utilize this node as much as possible**.</span></span>
    
     <span data-ttu-id="bfd3d-158">Op dit moment eruit uw formulier enigszins vergelijkbaar met het volgende:</span><span class="sxs-lookup"><span data-stu-id="bfd3d-158">At this point, your form would look somewhat similar to this:</span></span>
    
     ![De sjabloonconfiguratie][template config]
13. <span data-ttu-id="bfd3d-160">In **installatiekopie familie-Id of** u moet opgeven welke installatiekopie wordt geïnstalleerd op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-160">In **Image Family or Id** you have to specify what system image will be installed on your VM.</span></span> <span data-ttu-id="bfd3d-161">U kunt selecteren in een lijst van families van de afbeelding of geef een aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-161">You can either select from a list of image families or specify a custom image.</span></span>
    
     <span data-ttu-id="bfd3d-162">Als u selecteren in een lijst van families van de installatiekopie wilt, voert u het eerste teken (hoofdlettergevoelig) van de naam van de installatiekopie-serie.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-162">If you want to select from a list of image families, enter the first character (case-sensitive) of the image family name.</span></span> <span data-ttu-id="bfd3d-163">Voor het exemplaar typen **U** verschijnt nu een lijst met Ubuntu Server families.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-163">For instance, typing **U** will bring up a list of Ubuntu Server families.</span></span> <span data-ttu-id="bfd3d-164">Wanneer u in de lijst selecteert, wordt Jenkins de nieuwste versie van deze installatiekopie van die familie gebruiken bij het inrichten van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-164">Once you select from the list, Jenkins will use the latest version of that system image from that family when provisioning your VM.</span></span>
    
     ![Lijst met familie van besturingssystemen][OS family list]
    
     <span data-ttu-id="bfd3d-166">Als u een aangepaste installatiekopie die u wilt gebruiken in plaats daarvan hebt, voer de naam van de aangepaste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-166">If you have a custom image that you want to use instead, enter the name of that custom image.</span></span> <span data-ttu-id="bfd3d-167">Afbeelding van aangepaste namen worden niet weergegeven in een lijst zodat u ervoor te zorgen dat de naam correct worden ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-167">Custom image names are not shown in a list so you have to ensure that the name is entered correctly.</span></span>    
    
     <span data-ttu-id="bfd3d-168">Typ voor deze zelfstudie **U** online zetten van een lijst met afbeeldingen Ubuntu en selecteer **Ubuntu Server 14.04 TNS**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-168">For this tutorial, type **U** to bring up a list of Ubuntu images and select **Ubuntu Server 14.04 LTS**.</span></span>
14. <span data-ttu-id="bfd3d-169">Voor **methode starten**, selecteer **SSH**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-169">For **Launch method**, select **SSH**.</span></span>
15. <span data-ttu-id="bfd3d-170">Het onderstaande script kopiëren en plakken in de **Init script** veld.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-170">Copy the script below and paste in the **Init script** field.</span></span>
    
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
    
     <span data-ttu-id="bfd3d-171">De **Init script** worden uitgevoerd nadat de virtuele machine is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-171">The **Init script** will be executed after the VM is created.</span></span> <span data-ttu-id="bfd3d-172">In dit voorbeeld installeert het script Java, git en ant.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-172">In this example, the script installs Java, git, and ant.</span></span>
16. <span data-ttu-id="bfd3d-173">In de **gebruikersnaam** en **wachtwoord** velden, voert u de gewenste waarden voor de administrator-account dat wordt gemaakt op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-173">In the **Username** and **Password** fields, enter your preferred values for the administrator account that will be created on your VM.</span></span>
17. <span data-ttu-id="bfd3d-174">Klik op **sjabloon controleren** om te controleren of de parameters die u hebt opgegeven ongeldig zijn.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-174">Click on **Verify Template** to check if the parameters you specified are valid.</span></span>
18. <span data-ttu-id="bfd3d-175">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-175">Click on **Save**.</span></span>

## <a name="create-a-hudson-job-that-runs-on-a-slave-node-on-azure"></a><span data-ttu-id="bfd3d-176">Een taak Hudson die wordt uitgevoerd op een lager niveau bevindende-knooppunt in Azure maken</span><span class="sxs-lookup"><span data-stu-id="bfd3d-176">Create a Hudson job that runs on a slave node on Azure</span></span>
<span data-ttu-id="bfd3d-177">In deze sectie maakt u een Hudson-taak die wordt uitgevoerd op een knooppunt slave op Azure.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-177">In this section, you'll be creating a Hudson task that will run on a slave node on Azure.</span></span>

1. <span data-ttu-id="bfd3d-178">Klik in het dashboard Hudson **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-178">In the Hudson dashboard, click **New Job**.</span></span>
2. <span data-ttu-id="bfd3d-179">Voer een naam voor de taak die u maakt.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-179">Enter a name for the job you are creating.</span></span>
3. <span data-ttu-id="bfd3d-180">Selecteer voor het taaktype **bouwen van een taak vrije-stijl software**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-180">For the job type, select **Build a free-style software job**.</span></span>
4. <span data-ttu-id="bfd3d-181">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-181">Click **OK**.</span></span>
5. <span data-ttu-id="bfd3d-182">Selecteer in de configuratiepagina van de taak **beperken waar dit project kan worden uitgevoerd**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-182">In the job configuration page, select **Restrict where this project can be run**.</span></span>
6. <span data-ttu-id="bfd3d-183">Selecteer **knooppunt en label menu** en selecteer **linux** (we opgegeven dit label bij het maken van de virtuele machine-sjabloon in de vorige sectie).</span><span class="sxs-lookup"><span data-stu-id="bfd3d-183">Select **Node and label menu** and select **linux** (we specified this label when creating the virtual machine template in the previous section).</span></span>
7. <span data-ttu-id="bfd3d-184">In de **bouwen** sectie, klikt u op **toevoegen build stap** en selecteer **shell uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-184">In the **Build** section, click **Add build step** and select **Execute shell**.</span></span>
8. <span data-ttu-id="bfd3d-185">Bewerken van het volgende script, vervangen **{uw github-accountnaam}**, **{projectnaam van uw}**, en **{uw projectmap}** met waarden nodig en plak het bewerkte het script in het tekstgebied die wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-185">Edit the following script, replacing **{your github account name}**, **{your project name}**, and **{your project directory}** with appropriate values, and paste the edited script in the text area that appears.</span></span>
   
        # Clone from git repo
   
        currentDir="$PWD"
   
        if [ -e {your project directory} ]; then
   
              cd {your project directory}
   
              git pull origin master
   
        else
   
              git clone https://github.com/{your github account name}/{your project name}.git
   
        fi
   
        # change directory to project
   
        cd $currentDir/{your project directory}
   
        #Execute build task
   
        ant
9. <span data-ttu-id="bfd3d-186">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-186">Click on **Save**.</span></span>
10. <span data-ttu-id="bfd3d-187">Zoek in het dashboard Hudson de taak die u zojuist hebt gemaakt en klik op de **plannen van een build** pictogram.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-187">In the Hudson dashboard, find the job you just created and click on the **Schedule a build** icon.</span></span>

<span data-ttu-id="bfd3d-188">Hudson vervolgens maakt u een lager niveau bevindende knooppunt met behulp van de sjabloon in de vorige sectie hebt gemaakt en voer het script dat u hebt opgegeven in de stap build voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-188">Hudson will then create a slave node using the template created in the previous section and execute the script you specified in the build step for this task.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfd3d-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfd3d-189">Next Steps</span></span>
<span data-ttu-id="bfd3d-190">In het [Azure Java Developer Center] vindt u meer informatie over het gebruik van Azure met Java.</span><span class="sxs-lookup"><span data-stu-id="bfd3d-190">For more information about using Azure with Java, see the [Azure Java Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="bfd3d-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="bfd3d-191">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="bfd3d-192">[abonnement profiel]: http://go.microsoft.com/fwlink/?LinkID=396395</span><span class="sxs-lookup"><span data-stu-id="bfd3d-192">[subscription profile]: http://go.microsoft.com/fwlink/?LinkID=396395</span></span>

<!-- IMG List -->

[add new cloud]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addcloud.png
[configure profile]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-configureprofile.png
[add vm template]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-addnewvmtemplate.png
[template config]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-setup-templateconfig1-withdata.png
[OS family list]: ./media/virtual-machines-azure-slave-plugin-for-hudson/hudson-oslist.png

