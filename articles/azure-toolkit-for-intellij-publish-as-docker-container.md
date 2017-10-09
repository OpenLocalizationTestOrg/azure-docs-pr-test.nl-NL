---
title: een Docker-container met behulp van aaaPublish hello Azure Toolkit voor IntelliJ | Microsoft Docs
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a><span data-ttu-id="e9c5c-103">Een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="e9c5c-103">Publish a web app as a Docker container by using hello Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="e9c5c-104">Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="e9c5c-105">Met behulp van Docker-containers kunnen ontwikkelaars alle projectbestanden en afhankelijkheden in een enkel pakket voor tooa implementatieserver consolideren.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="e9c5c-106">Hello Azure Toolkit voor IntelliJ vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* functies voor implementatie tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-106">hello Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="e9c5c-107">Dit artikel begeleidt u bij Hallo stappen vereist toopublish uw toepassingen tooAzure als Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e9c5c-108">Meer informatie over Docker is beschikbaar op Hallo [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="e9c5c-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="e9c5c-109">Uw web-app tooAzure publiceren met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="e9c5c-109">Publish your web app tooAzure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="e9c5c-110">toopublish uw web-app, moet u een implementatie-ready artefacten maken.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-110">toopublish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="e9c5c-111">meer, Zie Hallo toolearn [aanvullende informatie over het maken van artefacten](#artifacts) sectie.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-111">toolearn more, see hello [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="e9c5c-112">Nadat u de wizard implementatie Hallo ten minste eenmaal hebt voltooid, worden de meeste van uw instellingen als standaardwaarden gebruikt wanneer u Hallo wizard opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-112">After you have completed hello deployment wizard at least once, most of your settings are used as defaults when you run hello wizard again.</span></span>
>

1. <span data-ttu-id="e9c5c-113">Open IntelliJ uw web-app-project.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="e9c5c-114">Hallo toostart **publiceren als Docker-Container** wizard Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-114">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="e9c5c-115">In Hallo **Project** venster hulpprogramma, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-115">In hello **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Hallo publiceren als de opdracht Docker-Container][PUB01]

   * <span data-ttu-id="e9c5c-117">Klik op Hallo IntelliJ werkbalk op Hallo **groep publiceren** knop en klik vervolgens op **publiceren als Docker-Container**:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-117">On hello IntelliJ toolbar, click hello **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="e9c5c-118">![Hallo publiceren als de opdracht Docker-Container][PUB02]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-118">![hello Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="e9c5c-119">Hallo **Docker-Container in Azure implementeren** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-119">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![Hallo Docker-Container in de wizard Azure implementeren][PUB03]

3. <span data-ttu-id="e9c5c-121">In Hallo **typt u een installatiekopie met de naam, selecteer Hallo-artefact pad en controleren van een Docker host toobe gebruikt** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-121">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span> 

   <span data-ttu-id="e9c5c-122">a.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-122">a.</span></span> <span data-ttu-id="e9c5c-123">In Hallo **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-123">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="e9c5c-124">(Hallo wizard maakt automatisch een naam, maar u kunt deze wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="e9c5c-124">(hello wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="e9c5c-125">b.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-125">b.</span></span> <span data-ttu-id="e9c5c-126">Hallo **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-126">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="e9c5c-127">Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-127">Do either of hello following:</span></span> 
      * <span data-ttu-id="e9c5c-128">Als u een bestaande Docker-host hebt, kunt u uw web-app tooit kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-128">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
      * <span data-ttu-id="e9c5c-129">toocreate een Docker-host, klikt u op Hallo groen plusteken (**+**).</span><span class="sxs-lookup"><span data-stu-id="e9c5c-129">toocreate a Docker host, click hello green plus sign (**+**).</span></span>  
       <span data-ttu-id="e9c5c-130">Hallo **Docker-Host maken** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-130">hello **Create Docker Host** dialog box opens.</span></span> 

      ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. <span data-ttu-id="e9c5c-132">In Hallo **Hallo nieuwe virtuele machine configureren** venster bieden Hallo informatie over de Docker-host te volgen.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-132">In hello **Configure hello new virtual machine** window, provide hello following information about your Docker host.</span></span> <span data-ttu-id="e9c5c-133">(Hallo wizard genereert automatisch Hallo-informatie voor u de meeste, maar u deze kunt wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="e9c5c-133">(hello wizard automatically generates most of hello information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="e9c5c-134">a.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-134">a.</span></span> <span data-ttu-id="e9c5c-135">In Hallo **naam** Voer een unieke naam voor Hallo Docker-host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-135">In hello **Name** box, enter a unique name for hello Docker host.</span></span> <span data-ttu-id="e9c5c-136">(Dit is hetzelfde als de naam van de Docker-installatiekopie die u eerder hebt opgegeven Hallo niet Hallo.)</span><span class="sxs-lookup"><span data-stu-id="e9c5c-136">(It is not hello same as hello Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="e9c5c-137">b.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-137">b.</span></span> <span data-ttu-id="e9c5c-138">In Hallo **abonnement** Voer hello Azure-abonnement dat u voor de host gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-138">In hello **Subscription** box, enter hello Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="e9c5c-139">c.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-139">c.</span></span> <span data-ttu-id="e9c5c-140">In Hallo **regio** Voer Hallo geografische regio waar uw host bevindt.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-140">In hello **Region** box, enter hello geographical region where your host is located.</span></span>
      
   <span data-ttu-id="e9c5c-141">d.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-141">d.</span></span> <span data-ttu-id="e9c5c-142">Op Hallo **OS en de grootte** tabblad, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-142">On hello **OS and Size** tab, do hello following:</span></span>      
      * <span data-ttu-id="e9c5c-143">**Host-OS**: Voer Hallo-besturingssysteem voor Hallo virtuele machine met de host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-143">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="e9c5c-144">**De grootte van**: Geef de grootte voor de virtuele machine Hallo voor de host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-144">**Size**: Enter hello virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="e9c5c-145">e.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-145">e.</span></span> <span data-ttu-id="e9c5c-146">Op Hallo **resourcegroep** tabblad, selecteert u een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-146">On hello **Resource Group** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="e9c5c-147">**Nieuwe resourcegroep**: een resourcegroep maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="e9c5c-148">**Bestaande resourcegroep**: Geef een bestaande resourcegroep van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="e9c5c-149">f.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-149">f.</span></span> <span data-ttu-id="e9c5c-150">Op Hallo **netwerk** tabblad, selecteert u een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-150">On hello **Network** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="e9c5c-151">**Nieuw virtueel netwerk**: een virtueel netwerk maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="e9c5c-152">**Bestaand virtueel netwerk**: Geef een bestaand virtueel netwerk van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="e9c5c-153">g.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-153">g.</span></span> <span data-ttu-id="e9c5c-154">Op Hallo **opslag** tabblad, selecteert u een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-154">On hello **Storage** tab, select either of hello following:</span></span>      
      * <span data-ttu-id="e9c5c-155">**Nieuw opslagaccount**: een opslagaccount maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="e9c5c-156">**Bestaande opslagaccount**: Geef een bestaand opslagaccount van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="e9c5c-157">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-157">Click **Next**.</span></span>  
     <span data-ttu-id="e9c5c-158">Hallo **logboek referenties configureren en poortinstellingen** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-158">hello **Configure log in credentials and port settings** window opens.</span></span>

      ![Hallo configureren aanmelden referenties en poort instellingenvenster][PUB05]

6. <span data-ttu-id="e9c5c-160">Selecteer een Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-160">Select one of hello following options:</span></span>

      * <span data-ttu-id="e9c5c-161">**Referenties importeren uit Azure Key Vault**: Geef een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="e9c5c-162">Een Azure sleutelkluis die gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die Hallo-abonnement deelt.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="e9c5c-163">tooallow een ander account of de service principal toouse Hallo key vault, moet u hello Azure portal tooadd Hallo account of service-principal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-163">tooallow another account or service principal toouse hello key vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

      * <span data-ttu-id="e9c5c-164">**Nieuwe aanmelding referenties**: Maak een nieuwe set aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="e9c5c-165">Als u deze optie selecteert, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-165">If you select this option, do hello following:</span></span>

        <span data-ttu-id="e9c5c-166">a.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-166">a.</span></span> <span data-ttu-id="e9c5c-167">Op Hallo **VM referenties** tabblad, bieden Hallo-gegevens voor Hallo aanmeldingsgegevens voor virtuele machines van de Docker-host te volgen: * **gebruikersnaam**: Hallo gebruikersnaam invoeren voor de aanmelding voor uw virtuele machines de referenties.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-167">On hello **VM Credentials** tab, provide hello following information for hello virtual-machine login credentials of your Docker host: * **Username**: Enter hello username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="e9c5c-168">* **Wachtwoord** en **bevestigen**: Hallo wachtwoord invoeren voor uw virtuele machines aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-168">* **Password** and **Confirm**: Enter hello password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="e9c5c-169">* **SSH**: Voer Hallo Secure Shell (SSH)-instellingen voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-169">* **SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="e9c5c-170">U kunt een Hallo volgende opties selecteren: * **geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-170">You can select one of hello following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="e9c5c-171">* **Automatisch genereren**: automatisch maakt Hallo vereiste instellingen voor verbinding maken via SSH.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-171">* **Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="e9c5c-172">* **Importeren uit directory**: Hiermee kunt u toospecify een map met een set van de eerder opgeslagen SSH-instellingen.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-172">* **Import from directory**: Allows you toospecify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="e9c5c-173">Hallo directory moet de volgende twee bestanden Hallo bevatten:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-173">hello directory must contain hello following two files:</span></span>
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        <span data-ttu-id="e9c5c-174">b.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-174">b.</span></span> <span data-ttu-id="e9c5c-175">Op Hallo **Docker-Daemon toegang** tabblad, bieden Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-175">On hello **Docker Daemon Access** tab, provide hello following information:</span></span>

          ![Docker-Host maken][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="e9c5c-177">Nadat u Hallo vereiste gegevens hebt ingevoerd, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-177">After you have entered hello required information, click **Finish**.</span></span>  
    <span data-ttu-id="e9c5c-178">Hallo **Docker-Container in Azure implementeren** wizard opnieuw wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-178">hello **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Docker-Container in de Wizard Azure implementeren][PUB07]

8. <span data-ttu-id="e9c5c-180">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-180">Click **Next**.</span></span>  
    <span data-ttu-id="e9c5c-181">Hallo **hello Docker-container toobe gemaakt configureren** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-181">hello **Configure hello Docker container toobe created** window opens.</span></span>

   ![Hallo configureren Hallo Docker-container gemaakt toobe venster][PUB08]

9. <span data-ttu-id="e9c5c-183">In Hallo **hello Docker-container toobe gemaakt configureren** venster bieden Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-183">In hello **Configure hello Docker container toobe created** window, provide hello following information:</span></span> 

   <span data-ttu-id="e9c5c-184">a.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-184">a.</span></span> <span data-ttu-id="e9c5c-185">In Hallo **Docker-containernaam** Voer een unieke naam voor uw Docker-container.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-185">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="e9c5c-186">b.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-186">b.</span></span> <span data-ttu-id="e9c5c-187">Kies een van de Hallo Docker-installatiekopieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-187">Choose one of hello following Docker images:</span></span> 

      * <span data-ttu-id="e9c5c-188">**De installatiekopie van een vooraf gedefinieerde Docker**: Geef een bestaande Docker-installatiekopie uit Azure.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="e9c5c-189">Hallo-lijst van Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die Azure Toolkit is Hallo toopatch zo geconfigureerd dat uw artefacten automatisch wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-189">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="e9c5c-190">**Aangepaste Dockerfile**: Geef een eerder opgeslagen Dockerfile vanaf uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="e9c5c-191">Dit is een geavanceerde functie voor ontwikkelaars die toodeploy hun eigen Dockerfile willen.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-191">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="e9c5c-192">Het is echter van toodevelopers die gebruikmaken van deze optie tooensure die hun Dockerfile correct is ingebouwd.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-192">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="e9c5c-193">Omdat Azure Toolkit Hallo Hallo inhoud in een aangepaste Dockerfile niet valideren, worden de Hallo-implementatie kan mislukken als Hallo Dockerfile problemen heeft.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-193">Because hello Azure Toolkit does not validate hello content in a custom Dockerfile, hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="e9c5c-194">Bovendien omdat hello Azure Toolkit Hallo aangepaste Dockerfile toocontain een artefact van web-app verwacht, probeert het tooopen een HTTP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-194">In addition, because hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, it attempts tooopen an HTTP connection.</span></span> <span data-ttu-id="e9c5c-195">Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="e9c5c-196">c.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-196">c.</span></span> <span data-ttu-id="e9c5c-197">In Hallo **poortinstellingen** Voer Hallo unieke TCP-poortbinding voor de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-197">In hello **Port settings** box, enter hello unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="e9c5c-198">Nadat u Hallo vorige stappen hebt voltooid, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-198">After you have completed hello preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="e9c5c-199">Hello Azure Toolkit begint de tooAzure van uw web-app in een Docker-container te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-199">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> <span data-ttu-id="e9c5c-200">Tenzij u hebt geconfigureerd IntelliJ toobe geïmplementeerd op de achtergrond hello, een **tooAzure implementeren** voortgangsbalk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-200">Unless you have configured IntelliJ toobe deployed in hello background, a **Deploying tooAzure** progress bar appears.</span></span> 

![Hallo implementatie voortgangsbalk][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="e9c5c-202">Als u meer informatie over het maken van artefacten</span><span class="sxs-lookup"><span data-stu-id="e9c5c-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="e9c5c-203">een artefact implementatie gereed toocreate Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-203">toocreate a deployment-ready artifact, do hello following:</span></span>

1. <span data-ttu-id="e9c5c-204">Open IntelliJ uw web-app-project.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="e9c5c-205">Klik op **bestand**, en klik vervolgens op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-205">Click **File**, and then click **Project Structure**.</span></span>

   ![Hallo structuur Project-opdracht][ART01]

3. <span data-ttu-id="e9c5c-207">tooadd een artefact, klikt u op Hallo groen plusteken (**+**), en klik vervolgens op **webtoepassing: archief**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-207">tooadd an artifact, click hello green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![Hallo 'Toepassing: webarchief'-opdracht][ART02]

4. <span data-ttu-id="e9c5c-209">In Hallo **naam** Voer een naam voor uw artefacten (omvatten geen Hallo *.war* extensie), en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-209">In hello **Name** box, enter a name for your artifact (do not include hello *.war* extension), and then click **OK**.</span></span>

   ![Hallo artefact naamvak][ART03]

<span data-ttu-id="e9c5c-211">Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op Hallo JetBrains website.</span><span class="sxs-lookup"><span data-stu-id="e9c5c-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on hello JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9c5c-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9c5c-212">Next steps</span></span>
<span data-ttu-id="e9c5c-213">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="e9c5c-213">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="e9c5c-214">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9c5c-215">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-215">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9c5c-216">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-216">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9c5c-217">[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-217">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="e9c5c-218">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="e9c5c-219">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="e9c5c-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9c5c-220">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-220">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9c5c-221">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-221">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9c5c-222">[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-222">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="e9c5c-223">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="e9c5c-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="e9c5c-224">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e9c5c-224">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e9c5c-225">Zie voor aanvullende bronnen voor Docker Hallo officiële [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="e9c5c-225">For additional resources for Docker, see hello official [Docker website].</span></span>

<!-- URL List -->

[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md
[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)
[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Hello Azure Toolkit voor Eclipse installeren]: ./azure-toolkit-for-eclipse-installation.md
[Hello Azure Toolkit voor IntelliJ installeren]: ./azure-toolkit-for-intellij-installation.md
[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Wat is er nieuw in hello Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/

[Docker-website]: https://www.docker.com/
[artefacten configureren]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
