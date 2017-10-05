---
title: Een Docker-container te publiceren met behulp van de Azure-Toolkit voor IntelliJ | Microsoft Docs
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 96680319a6c4c0f0a4673cd6303a5b172f428797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-intellij"></a><span data-ttu-id="c0e05-103">Een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor IntelliJ</span><span class="sxs-lookup"><span data-stu-id="c0e05-103">Publish a web app as a Docker container by using the Azure Toolkit for IntelliJ</span></span>

<span data-ttu-id="c0e05-104">Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="c0e05-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="c0e05-105">Met behulp van Docker-containers kunnen ontwikkelaars hun project-bestanden en afhankelijkheden in een enkel pakket voor implementatie naar een server consolideren.</span><span class="sxs-lookup"><span data-stu-id="c0e05-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="c0e05-106">De Azure-werkset voor IntelliJ vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* onderdelen voor implementatie naar Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e05-106">The Azure Toolkit for IntelliJ simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="c0e05-107">Dit artikel begeleidt u bij de stappen die nodig zijn voor het publiceren van uw toepassingen naar Azure als Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="c0e05-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
>
> <span data-ttu-id="c0e05-108">Meer informatie over Docker is beschikbaar op de [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="c0e05-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="c0e05-109">Uw web-app publiceren naar Azure met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="c0e05-109">Publish your web app to Azure by using a Docker container</span></span>

> [!NOTE]
> * <span data-ttu-id="c0e05-110">Voor het publiceren van uw web-app, moet u een artefact implementatie gereed te maken.</span><span class="sxs-lookup"><span data-stu-id="c0e05-110">To publish your web app, you must create a deployment-ready artifact.</span></span> <span data-ttu-id="c0e05-111">Zie voor meer informatie, de [aanvullende informatie over het maken van artefacten](#artifacts) sectie.</span><span class="sxs-lookup"><span data-stu-id="c0e05-111">To learn more, see the [Additional information about creating artifacts](#artifacts) section.</span></span>
>
> * <span data-ttu-id="c0e05-112">Nadat u de implementatiewizard ten minste eenmaal hebt voltooid, worden de meeste van uw instellingen als standaardwaarden gebruikt wanneer u de wizard opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c0e05-112">After you have completed the deployment wizard at least once, most of your settings are used as defaults when you run the wizard again.</span></span>
>

1. <span data-ttu-id="c0e05-113">Open IntelliJ uw web-app-project.</span><span class="sxs-lookup"><span data-stu-id="c0e05-113">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="c0e05-114">Starten de **publiceren als Docker-Container** wizard een van de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="c0e05-114">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="c0e05-115">In de **Project** venster hulpprogramma, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**:</span><span class="sxs-lookup"><span data-stu-id="c0e05-115">In the **Project** tool window, right-click your project, click **Azure**, and then click **Publish as Docker Container**:</span></span>

      ![Het publiceren als de opdracht Docker-Container][PUB01]

   * <span data-ttu-id="c0e05-117">Klik op de werkbalk IntelliJ de **groep publiceren** knop en klik vervolgens op **publiceren als Docker-Container**:</span><span class="sxs-lookup"><span data-stu-id="c0e05-117">On the IntelliJ toolbar, click the **Publish Group** button, and then click **Publish as Docker Container**:</span></span>

      <span data-ttu-id="c0e05-118">![Het publiceren als de opdracht Docker-Container][PUB02]</span><span class="sxs-lookup"><span data-stu-id="c0e05-118">![The Publish as Docker Container command][PUB02]</span></span>  
    <span data-ttu-id="c0e05-119">De **Docker-Container in Azure implementeren** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c0e05-119">The **Deploy Docker Container on Azure** wizard opens.</span></span>

   ![De Docker-Container implementeren in de Azure-wizard][PUB03]

3. <span data-ttu-id="c0e05-121">In de **typt u een installatiekopie met de naam, selecteer het artefact pad en controleren van een Docker-host moet worden gebruikt** venster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="c0e05-121">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span> 

   <span data-ttu-id="c0e05-122">a.</span><span class="sxs-lookup"><span data-stu-id="c0e05-122">a.</span></span> <span data-ttu-id="c0e05-123">In de **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-123">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="c0e05-124">(De wizard maakt automatisch een naam, maar u kunt deze wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="c0e05-124">(The wizard automatically creates a name, but you can modify it.)</span></span> 

   <span data-ttu-id="c0e05-125">b.</span><span class="sxs-lookup"><span data-stu-id="c0e05-125">b.</span></span> <span data-ttu-id="c0e05-126">De **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0e05-126">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="c0e05-127">Voer een van de volgende bewerkingen uit:</span><span class="sxs-lookup"><span data-stu-id="c0e05-127">Do either of the following:</span></span> 
      * <span data-ttu-id="c0e05-128">Als u een bestaande Docker-host hebt, kunt u uw web-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="c0e05-128">If you have an existing Docker host, you can deploy your web app to it.</span></span>
      * <span data-ttu-id="c0e05-129">Klik op het groen plusteken om een Docker-host (**+**).</span><span class="sxs-lookup"><span data-stu-id="c0e05-129">To create a Docker host, click the green plus sign (**+**).</span></span>  
       <span data-ttu-id="c0e05-130">De **Docker-Host maken** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c0e05-130">The **Create Docker Host** dialog box opens.</span></span> 

      ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. <span data-ttu-id="c0e05-132">In de **configureren van de nieuwe virtuele machine** venster de volgende informatie over de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-132">In the **Configure the new virtual machine** window, provide the following information about your Docker host.</span></span> <span data-ttu-id="c0e05-133">(De wizard automatisch de meeste informatie voor u gegenereerd, maar u deze kunt wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="c0e05-133">(The wizard automatically generates most of the information for you, but you can modify any of them.)</span></span> 

   <span data-ttu-id="c0e05-134">a.</span><span class="sxs-lookup"><span data-stu-id="c0e05-134">a.</span></span> <span data-ttu-id="c0e05-135">In de **naam** Voer een unieke naam voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-135">In the **Name** box, enter a unique name for the Docker host.</span></span> <span data-ttu-id="c0e05-136">(Dit is niet hetzelfde zijn als de naam van de Docker-installatiekopie die u eerder hebt opgegeven.)</span><span class="sxs-lookup"><span data-stu-id="c0e05-136">(It is not the same as the Docker image name that you specified earlier.)</span></span> 
    
   <span data-ttu-id="c0e05-137">b.</span><span class="sxs-lookup"><span data-stu-id="c0e05-137">b.</span></span> <span data-ttu-id="c0e05-138">In de **abonnement** Voer het Azure-abonnement dat u voor de host gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c0e05-138">In the **Subscription** box, enter the Azure subscription that you use for your host.</span></span> 
      
   <span data-ttu-id="c0e05-139">c.</span><span class="sxs-lookup"><span data-stu-id="c0e05-139">c.</span></span> <span data-ttu-id="c0e05-140">In de **regio** Voer de geografische regio waar uw host bevindt.</span><span class="sxs-lookup"><span data-stu-id="c0e05-140">In the **Region** box, enter the geographical region where your host is located.</span></span>
      
   <span data-ttu-id="c0e05-141">d.</span><span class="sxs-lookup"><span data-stu-id="c0e05-141">d.</span></span> <span data-ttu-id="c0e05-142">Op de **OS en de grootte** tabblad, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c0e05-142">On the **OS and Size** tab, do the following:</span></span>      
      * <span data-ttu-id="c0e05-143">**Host-OS**: Geef het besturingssysteem voor de virtuele machine die de host bevat.</span><span class="sxs-lookup"><span data-stu-id="c0e05-143">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span> 
      * <span data-ttu-id="c0e05-144">**De grootte van**: Geef de grootte van de virtuele machine voor de host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-144">**Size**: Enter the virtual-machine size for your host.</span></span>   
       
   <span data-ttu-id="c0e05-145">e.</span><span class="sxs-lookup"><span data-stu-id="c0e05-145">e.</span></span> <span data-ttu-id="c0e05-146">Op de **resourcegroep** tabblad, selecteert u een van de volgende:</span><span class="sxs-lookup"><span data-stu-id="c0e05-146">On the **Resource Group** tab, select either of the following:</span></span>      
      * <span data-ttu-id="c0e05-147">**Nieuwe resourcegroep**: een resourcegroep maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-147">**New resource group**: Create a resource group for your host.</span></span>
      * <span data-ttu-id="c0e05-148">**Bestaande resourcegroep**: Geef een bestaande resourcegroep van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c0e05-148">**Existing resource group**: Specify an existing resource group from your Azure account.</span></span> 
       
   <span data-ttu-id="c0e05-149">f.</span><span class="sxs-lookup"><span data-stu-id="c0e05-149">f.</span></span> <span data-ttu-id="c0e05-150">Op de **netwerk** tabblad, selecteert u een van de volgende:</span><span class="sxs-lookup"><span data-stu-id="c0e05-150">On the **Network** tab, select either of the following:</span></span>      
      * <span data-ttu-id="c0e05-151">**Nieuw virtueel netwerk**: een virtueel netwerk maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-151">**New virtual network**: Create a virtual network for your host.</span></span>
      * <span data-ttu-id="c0e05-152">**Bestaand virtueel netwerk**: Geef een bestaand virtueel netwerk van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c0e05-152">**Existing virtual network**: Specify an existing virtual network from your Azure account.</span></span> 
       
   <span data-ttu-id="c0e05-153">g.</span><span class="sxs-lookup"><span data-stu-id="c0e05-153">g.</span></span> <span data-ttu-id="c0e05-154">Op de **opslag** tabblad, selecteert u een van de volgende:</span><span class="sxs-lookup"><span data-stu-id="c0e05-154">On the **Storage** tab, select either of the following:</span></span>      
      * <span data-ttu-id="c0e05-155">**Nieuw opslagaccount**: een opslagaccount maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-155">**New storage account**: Create a storage account for your host.</span></span>
      * <span data-ttu-id="c0e05-156">**Bestaande opslagaccount**: Geef een bestaand opslagaccount van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c0e05-156">**Existing storage account**: Specify an existing storage account from your Azure account.</span></span>
       
5. <span data-ttu-id="c0e05-157">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-157">Click **Next**.</span></span>  
     <span data-ttu-id="c0e05-158">De **logboek referenties configureren en poortinstellingen** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c0e05-158">The **Configure log in credentials and port settings** window opens.</span></span>

      ![Het logboek configureren in de referenties en poort instellingenvenster][PUB05]

6. <span data-ttu-id="c0e05-160">Selecteer een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="c0e05-160">Select one of the following options:</span></span>

      * <span data-ttu-id="c0e05-161">**Referenties importeren uit Azure Key Vault**: Geef een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="c0e05-161">**Import credentials from Azure Key Vault**: Specify a previously saved set of credentials that are stored in your Azure subscription.</span></span>

          > [!NOTE]
          > <span data-ttu-id="c0e05-162">Een Azure sleutelkluis die gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die het abonnement deelt.</span><span class="sxs-lookup"><span data-stu-id="c0e05-162">An Azure key vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="c0e05-163">Als u wilt toestaan een ander account of -service principal gebruik van de sleutelkluis, moet u de Azure-portal de account of de service-principal toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="c0e05-163">To allow another account or service principal to use the key vault, you must use the Azure portal to add the account or service principal.</span></span>

      * <span data-ttu-id="c0e05-164">**Nieuwe aanmelding referenties**: Maak een nieuwe set aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="c0e05-164">**New log in credentials**: Create a new set of login credentials.</span></span> <span data-ttu-id="c0e05-165">Als u deze optie selecteert, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c0e05-165">If you select this option, do the following:</span></span>

        <span data-ttu-id="c0e05-166">a.</span><span class="sxs-lookup"><span data-stu-id="c0e05-166">a.</span></span> <span data-ttu-id="c0e05-167">Op de **VM referenties** tabblad, bieden de volgende informatie voor de virtuele machine-aanmeldingsreferenties van de Docker-host: * **gebruikersnaam**: Geef de gebruikersnaam voor uw virtuele machines aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="c0e05-167">On the **VM Credentials** tab, provide the following information for the virtual-machine login credentials of your Docker host: * **Username**: Enter the username for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="c0e05-168">* **Wachtwoord** en **bevestigen**: Voer het wachtwoord voor uw virtuele machines aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="c0e05-168">* **Password** and **Confirm**: Enter the password for your virtual-machine login credentials.</span></span>
             <span data-ttu-id="c0e05-169">* **SSH**: Geef de instellingen van Secure Shell (SSH) voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="c0e05-169">* **SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="c0e05-170">U kunt een van de volgende opties selecteren: * **geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="c0e05-170">You can select one of the following options: * **None**: Specifies that your virtual machine does not allow SSH connections.</span></span>
                <span data-ttu-id="c0e05-171">* **Automatisch genereren**: de vereiste instellingen automatisch maakt om verbinding te maken via SSH.</span><span class="sxs-lookup"><span data-stu-id="c0e05-171">* **Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
                <span data-ttu-id="c0e05-172">* **Importeren uit directory**: Hiermee kunt u een map met een set van de eerder opgeslagen SSH-instellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="c0e05-172">* **Import from directory**: Allows you to specify a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="c0e05-173">De map moet bevatten de volgende twee bestanden:</span><span class="sxs-lookup"><span data-stu-id="c0e05-173">The directory must contain the following two files:</span></span>
                
                  * *id_rsa*: Contains the RSA identification for a user.
                  * *id_rsa.pub*: Contains the RSA public key that is used for authentication.
            
        <span data-ttu-id="c0e05-174">b.</span><span class="sxs-lookup"><span data-stu-id="c0e05-174">b.</span></span> <span data-ttu-id="c0e05-175">Op de **Docker-Daemon toegang** tabblad, geef de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c0e05-175">On the **Docker Daemon Access** tab, provide the following information:</span></span>

          ![Docker-Host maken][PUB06]
    
             * **Docker Daemon port**: Enter the unique TCP port for your Docker host.
             * **TLS Security**: Enter the Transport Layer Security settings for your Docker host. You can choose from the following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates the requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. The directory must contain the following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain the client certificate and public key that is used for TLS authentication.

7. <span data-ttu-id="c0e05-177">Nadat u de vereiste gegevens hebt ingevoerd, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-177">After you have entered the required information, click **Finish**.</span></span>  
    <span data-ttu-id="c0e05-178">De **Docker-Container in Azure implementeren** wizard opnieuw wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0e05-178">The **Deploy Docker Container on Azure** wizard reappears.</span></span>

   ![Docker-Container in de Wizard Azure implementeren][PUB07]

8. <span data-ttu-id="c0e05-180">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-180">Click **Next**.</span></span>  
    <span data-ttu-id="c0e05-181">De **configureren de Docker-container gemaakt** venster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c0e05-181">The **Configure the Docker container to be created** window opens.</span></span>

   ![Het configureren van de Docker-container venster worden gemaakt][PUB08]

9. <span data-ttu-id="c0e05-183">In de **configureren de Docker-container gemaakt** venster de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c0e05-183">In the **Configure the Docker container to be created** window, provide the following information:</span></span> 

   <span data-ttu-id="c0e05-184">a.</span><span class="sxs-lookup"><span data-stu-id="c0e05-184">a.</span></span> <span data-ttu-id="c0e05-185">In de **Docker-containernaam** Voer een unieke naam voor uw Docker-container.</span><span class="sxs-lookup"><span data-stu-id="c0e05-185">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="c0e05-186">b.</span><span class="sxs-lookup"><span data-stu-id="c0e05-186">b.</span></span> <span data-ttu-id="c0e05-187">Kies een van de volgende Docker-afbeeldingen:</span><span class="sxs-lookup"><span data-stu-id="c0e05-187">Choose one of the following Docker images:</span></span> 

      * <span data-ttu-id="c0e05-188">**De installatiekopie van een vooraf gedefinieerde Docker**: Geef een bestaande Docker-installatiekopie uit Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e05-188">**Predefined Docker image**: Specify a pre-existing Docker image from Azure.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="c0e05-189">De lijst met Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die de Azure-Toolkit is geconfigureerd voor het patch zodat uw artefacten automatisch wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="c0e05-189">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span> 

      * <span data-ttu-id="c0e05-190">**Aangepaste Dockerfile**: Geef een eerder opgeslagen Dockerfile vanaf uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="c0e05-190">**Custom Dockerfile**: Specify a previously saved Dockerfile from your local computer.</span></span>

        > [!NOTE]
        > <span data-ttu-id="c0e05-191">Dit is een geavanceerde functie voor ontwikkelaars die willen hun eigen Dockerfile implementeren.</span><span class="sxs-lookup"><span data-stu-id="c0e05-191">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="c0e05-192">Het is echter maximaal ontwikkelaars die gebruikmaken van deze optie om ervoor te zorgen dat hun Dockerfile correct is gebouwd.</span><span class="sxs-lookup"><span data-stu-id="c0e05-192">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="c0e05-193">Omdat de Azure-Toolkit wordt de inhoud van een aangepaste Dockerfile niet gevalideerd, wordt de implementatie kan mislukken als de Dockerfile problemen heeft.</span><span class="sxs-lookup"><span data-stu-id="c0e05-193">Because the Azure Toolkit does not validate the content in a custom Dockerfile, the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="c0e05-194">Bovendien, omdat de Azure-Toolkit de aangepaste Dockerfile verwacht bevatten een web-app-artefacten, probeert te openen van een HTTP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="c0e05-194">In addition, because the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, it attempts to open an HTTP connection.</span></span> <span data-ttu-id="c0e05-195">Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="c0e05-195">If developers publish a different type of artifact, they might receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="c0e05-196">c.</span><span class="sxs-lookup"><span data-stu-id="c0e05-196">c.</span></span> <span data-ttu-id="c0e05-197">In de **poortinstellingen** Geef de unieke TCP-poort-binding voor de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="c0e05-197">In the **Port settings** box, enter the unique TCP port binding for your Docker container.</span></span> 

10. <span data-ttu-id="c0e05-198">Nadat u de voorgaande stappen hebt voltooid, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-198">After you have completed the preceding steps, click **Finish**.</span></span> 

<span data-ttu-id="c0e05-199">De Toolkit Azure begint uw web-app implementeren naar Azure in een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="c0e05-199">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> <span data-ttu-id="c0e05-200">Tenzij u hebt geconfigureerd IntelliJ worden geïmplementeerd op de achtergrond een **implementeren naar Azure** voortgangsbalk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c0e05-200">Unless you have configured IntelliJ to be deployed in the background, a **Deploying to Azure** progress bar appears.</span></span> 

![De voortgangsbalk implementatie][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a><span data-ttu-id="c0e05-202">Als u meer informatie over het maken van artefacten</span><span class="sxs-lookup"><span data-stu-id="c0e05-202">Additional information about creating artifacts</span></span>

<span data-ttu-id="c0e05-203">Voor het maken van een implementatie-gereed-artefacten, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="c0e05-203">To create a deployment-ready artifact, do the following:</span></span>

1. <span data-ttu-id="c0e05-204">Open IntelliJ uw web-app-project.</span><span class="sxs-lookup"><span data-stu-id="c0e05-204">Open your web app project in IntelliJ.</span></span>

2. <span data-ttu-id="c0e05-205">Klik op **bestand**, en klik vervolgens op **projectstructuur**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-205">Click **File**, and then click **Project Structure**.</span></span>

   ![De structuur van de Project-opdracht][ART01]

3. <span data-ttu-id="c0e05-207">Klik op Help als u een artefact groen plusteken (**+**), en klik vervolgens op **webtoepassing: archief**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-207">To add an artifact, click the green plus sign (**+**), and then click **Web Application: Archive**.</span></span>

   ![De opdracht 'Toepassing: webarchief'][ART02]

4. <span data-ttu-id="c0e05-209">In de **naam** Voer een naam voor uw artefacten (omvatten geen de *.war* extensie), en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c0e05-209">In the **Name** box, enter a name for your artifact (do not include the *.war* extension), and then click **OK**.</span></span>

   ![Het naamvak artefact][ART03]

<span data-ttu-id="c0e05-211">Zie voor meer informatie over het maken van artefacten in IntelliJ [artefacten configureren] op de website JetBrains.</span><span class="sxs-lookup"><span data-stu-id="c0e05-211">For more information about creating artifacts in IntelliJ, see [Configuring artifacts] on the JetBrains website.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0e05-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0e05-212">Next steps</span></span>
<span data-ttu-id="c0e05-213">Zie de volgende bronnen voor meer informatie over de Azure-Toolkits voor IDE voor Java:</span><span class="sxs-lookup"><span data-stu-id="c0e05-213">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="c0e05-214">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0e05-214">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c0e05-215">[Wat is er nieuw in de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0e05-215">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c0e05-216">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="c0e05-216">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c0e05-217">[Aanmelden instructies voor de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0e05-217">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c0e05-218">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c0e05-218">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c0e05-219">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c0e05-219">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c0e05-220">[Wat is er nieuw in de Azure-werkset voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c0e05-220">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c0e05-221">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="c0e05-221">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c0e05-222">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c0e05-222">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c0e05-223">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c0e05-223">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c0e05-224">Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c0e05-224">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="c0e05-225">Zie voor aanvullende bronnen voor Docker de officiële [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="c0e05-225">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="c0e05-226">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-226">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="c0e05-227">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="c0e05-227">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="c0e05-228">[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-228">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c0e05-229">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-229">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="c0e05-230">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="c0e05-230">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="c0e05-231">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="c0e05-231">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="c0e05-232">[Aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-232">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="c0e05-233">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-233">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="c0e05-234">[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-234">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="c0e05-235">[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="c0e05-235">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="c0e05-236">[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="c0e05-236">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="c0e05-237">[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="c0e05-237">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="c0e05-238">[Docker-website]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="c0e05-238">[Docker website]: https://www.docker.com/</span></span>
<span data-ttu-id="c0e05-239">[artefacten configureren]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span><span class="sxs-lookup"><span data-stu-id="c0e05-239">[Configuring artifacts]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html</span></span>

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
