---
title: Een Docker-container te publiceren met behulp van de Azure-Toolkit voor Eclipse | Microsoft Docs
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 746bb0a073396b84fa8592adda6748a2a5692ee8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-the-azure-toolkit-for-eclipse"></a><span data-ttu-id="5407a-103">Een web-app publiceren als een Docker-container met behulp van de Azure-Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="5407a-103">Publish a web app as a Docker container by using the Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="5407a-104">Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="5407a-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="5407a-105">Met behulp van Docker-containers kunnen ontwikkelaars hun project-bestanden en afhankelijkheden in een enkel pakket voor implementatie naar een server consolideren.</span><span class="sxs-lookup"><span data-stu-id="5407a-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment to a server.</span></span> <span data-ttu-id="5407a-106">De Azure-werkset voor Eclipse vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* onderdelen voor implementatie naar Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="5407a-106">The Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment to Microsoft Azure.</span></span> <span data-ttu-id="5407a-107">Dit artikel begeleidt u bij de stappen die nodig zijn voor het publiceren van uw toepassingen naar Azure als Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="5407a-107">This article walks you through the steps required to publish your applications to Azure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="5407a-108">Meer informatie over Docker is beschikbaar op de [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="5407a-108">More information about Docker is available on the [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-to-azure-by-using-a-docker-container"></a><span data-ttu-id="5407a-109">Uw web-app publiceren naar Azure met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="5407a-109">Publish your web app to Azure by using a Docker container</span></span>

1. <span data-ttu-id="5407a-110">Open uw web-app-project in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="5407a-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="5407a-111">Starten de **publiceren als Docker-Container** wizard een van de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="5407a-111">To start the **Publish as Docker Container** wizard, do either of the following:</span></span>

   * <span data-ttu-id="5407a-112">In de **Navigator** weergeven, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="5407a-112">In the **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Weergave van de Navigator publiceren als de opdracht Docker-Container][PUB01]

   * <span data-ttu-id="5407a-114">Klik op de werkbalk van Eclipse op de **publiceren** knop en klik vervolgens op **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="5407a-114">On the Eclipse toolbar, click the **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Werkbalk van eclipse publiceren als de opdracht Docker-Container][PUB02]
      
    <span data-ttu-id="5407a-116">De **Docker-Container in Azure implementeren** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5407a-116">The **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![De Docker-Container implementeren in de Azure-wizard][PUB03]

3. <span data-ttu-id="5407a-118">In de **typt u een installatiekopie met de naam, selecteer het artefact pad en controleren van een Docker-host moet worden gebruikt** venster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="5407a-118">In the **Type an image name, select the artifact's path and check a Docker host to be used** window, do the following:</span></span>

    <span data-ttu-id="5407a-119">a.</span><span class="sxs-lookup"><span data-stu-id="5407a-119">a.</span></span> <span data-ttu-id="5407a-120">In de **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="5407a-120">In the **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="5407a-121">(De wizard maakt automatisch een naam, maar u kunt deze wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="5407a-121">(The wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="5407a-122">b.</span><span class="sxs-lookup"><span data-stu-id="5407a-122">b.</span></span> <span data-ttu-id="5407a-123">De **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5407a-123">The **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="5407a-124">Voer een van de volgende bewerkingen uit:</span><span class="sxs-lookup"><span data-stu-id="5407a-124">Do either of the following:</span></span>

    * <span data-ttu-id="5407a-125">Als u een bestaande Docker-host hebt, kunt u uw web-app te implementeren.</span><span class="sxs-lookup"><span data-stu-id="5407a-125">If you have an existing Docker host, you can deploy your web app to it.</span></span>
    * <span data-ttu-id="5407a-126">Klik op om een nieuwe Docker-host **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="5407a-126">To create a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="5407a-127">De **Docker-Host maken** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5407a-127">The **Create Docker Host** dialog box opens.</span></span>

    ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. <span data-ttu-id="5407a-129">In de **configureren van de nieuwe virtuele machine** venster de volgende opties voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="5407a-129">In the **Configure the new virtual machine** window, specify the following options for your Docker host.</span></span> <span data-ttu-id="5407a-130">(De wizard wordt automatisch gegenereerd voor de meeste opties voor u, maar u kunt een van deze wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="5407a-130">(The wizard automatically generates most of the options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="5407a-131">a.</span><span class="sxs-lookup"><span data-stu-id="5407a-131">a.</span></span> <span data-ttu-id="5407a-132">**Naam**: Voer een unieke naam voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="5407a-132">**Name**: Enter a unique name for the Docker host.</span></span> <span data-ttu-id="5407a-133">(Dit is niet hetzelfde zijn als de naam van de Docker-installatiekopie die u eerder hebt opgegeven.)</span><span class="sxs-lookup"><span data-stu-id="5407a-133">(It is not the same as the Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="5407a-134">b.</span><span class="sxs-lookup"><span data-stu-id="5407a-134">b.</span></span> <span data-ttu-id="5407a-135">**Abonnement**: Voer het Azure-abonnement dat u voor de host gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5407a-135">**Subscription**: Enter the Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="5407a-136">c.</span><span class="sxs-lookup"><span data-stu-id="5407a-136">c.</span></span> <span data-ttu-id="5407a-137">**Regio**: Voer de geografische regio waar uw host bevindt.</span><span class="sxs-lookup"><span data-stu-id="5407a-137">**Region**: Enter the geographical region where your host is located.</span></span>

   <span data-ttu-id="5407a-138">d.</span><span class="sxs-lookup"><span data-stu-id="5407a-138">d.</span></span> <span data-ttu-id="5407a-139">Op de **Host-OS en de grootte** tabblad:</span><span class="sxs-lookup"><span data-stu-id="5407a-139">On the **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="5407a-140">**Host-OS**: Geef het besturingssysteem voor de virtuele machine die de host bevat.</span><span class="sxs-lookup"><span data-stu-id="5407a-140">**Host OS**: Enter the operating system for the virtual machine that contains your host.</span></span>
     * <span data-ttu-id="5407a-141">**De grootte van**: Geef de grootte van de virtuele machine voor de host.</span><span class="sxs-lookup"><span data-stu-id="5407a-141">**Size**: Enter the virtual-machine size for your host.</span></span>

   <span data-ttu-id="5407a-142">e.</span><span class="sxs-lookup"><span data-stu-id="5407a-142">e.</span></span> <span data-ttu-id="5407a-143">Op de **resourcegroep** tabblad:</span><span class="sxs-lookup"><span data-stu-id="5407a-143">On the **Resource Group** tab:</span></span>
     * <span data-ttu-id="5407a-144">**Nieuwe resourcegroep**: een nieuwe resourcegroep maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="5407a-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="5407a-145">**Bestaande resourcegroep**: Voer een bestaande resourcegroep van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5407a-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="5407a-146">f.</span><span class="sxs-lookup"><span data-stu-id="5407a-146">f.</span></span> <span data-ttu-id="5407a-147">Op de **netwerk** tabblad:</span><span class="sxs-lookup"><span data-stu-id="5407a-147">On the **Network** tab:</span></span>
     * <span data-ttu-id="5407a-148">**Nieuw virtueel netwerk**: Maak een nieuw virtueel netwerk voor de host.</span><span class="sxs-lookup"><span data-stu-id="5407a-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="5407a-149">**Bestaand virtueel netwerk**: Voer een bestaand virtueel netwerk van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5407a-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="5407a-150">g.</span><span class="sxs-lookup"><span data-stu-id="5407a-150">g.</span></span> <span data-ttu-id="5407a-151">Op de **opslag** tabblad:</span><span class="sxs-lookup"><span data-stu-id="5407a-151">On the **Storage** tab:</span></span>
     * <span data-ttu-id="5407a-152">**Nieuw opslagaccount**: Maak een nieuw opslagaccount voor de host.</span><span class="sxs-lookup"><span data-stu-id="5407a-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="5407a-153">**Bestaande opslagaccount**: Voer een bestaand opslagaccount van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="5407a-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="5407a-154">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="5407a-154">Click **Next**.</span></span>

6. <span data-ttu-id="5407a-155">In de **logboek referenties configureren en poortinstellingen** venster, selecteert u een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5407a-155">In the **Configure log in credentials and port settings** window, select one of the following options:</span></span>

    * <span data-ttu-id="5407a-156">**Referenties importeren uit Azure Key Vault**: Hiermee geeft u een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5407a-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="5407a-157">Een Azure Key Vault dat gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die het abonnement deelt.</span><span class="sxs-lookup"><span data-stu-id="5407a-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares the subscription.</span></span> <span data-ttu-id="5407a-158">Als u wilt toestaan een ander account of -service principal gebruik van de Sleutelkluis, moet u de Azure-portal de account of de service-principal toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="5407a-158">To allow another account or service principal to use the Key Vault, you must use the Azure portal to add the account or service principal.</span></span>

    * <span data-ttu-id="5407a-159">**Nieuwe aanmelding referenties**: maakt een nieuwe set aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="5407a-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="5407a-160">Als u deze optie selecteert, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="5407a-160">If you select this option, do the following:</span></span>
    
      * <span data-ttu-id="5407a-161">Op de **VM referenties** tabblad, kiest u een van de volgende opties voor de virtuele machine-aanmeldingsreferenties van de Docker-host:</span><span class="sxs-lookup"><span data-stu-id="5407a-161">On the **VM Credentials** tab, choose one of the following options for the virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="5407a-162">**Gebruikersnaam**: Geef de gebruikersnaam voor de aanmeldingsreferenties van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5407a-162">**Username**: Enter the username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="5407a-163">**Wachtwoord** en **bevestigen**: Voer het wachtwoord voor uw virtuele machine-aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="5407a-163">**Password** and **Confirm**: Enter the password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="5407a-164">**SSH**: Geef de instellingen van Secure Shell (SSH) voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="5407a-164">**SSH**: Enter the Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="5407a-165">U kunt kiezen uit de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5407a-165">You can choose from the following options:</span></span>
            * <span data-ttu-id="5407a-166">**Geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5407a-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="5407a-167">**Automatisch genereren**: de vereiste instellingen automatisch maakt om verbinding te maken via SSH.</span><span class="sxs-lookup"><span data-stu-id="5407a-167">**Auto-generate**: Automatically creates the requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="5407a-168">**Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen SSH-instellingen.</span><span class="sxs-lookup"><span data-stu-id="5407a-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="5407a-169">De map moet bevatten de volgende twee bestanden:</span><span class="sxs-lookup"><span data-stu-id="5407a-169">The directory must contain the following two files:</span></span>
                * <span data-ttu-id="5407a-170">*id_rsa*: bevat de RSA-id voor een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="5407a-170">*id_rsa*: Contains the RSA identification for a user.</span></span>
                * <span data-ttu-id="5407a-171">*id_rsa.pub*: bevat de openbare RSA-sleutel die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="5407a-171">*id_rsa.pub*: Contains the RSA public key that is used for authentication.</span></span>
        
        ![Docker-Host maken][PUB05]

      * <span data-ttu-id="5407a-173">Op de **Docker-Daemon referenties** tabblad, geeft u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5407a-173">On the **Docker Daemon Credentials** tab, specify the following options:</span></span>

          * <span data-ttu-id="5407a-174">**Docker-Daemon poort**: Voer de unieke TCP-poort voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="5407a-174">**Docker Daemon port**: Enter the unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="5407a-175">**TLS beveiliging**: Geef de Transport Layer Security-instellingen voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="5407a-175">**TLS Security**: Enter the Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="5407a-176">U kunt kiezen uit de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="5407a-176">You can choose from the following options:</span></span>
            * <span data-ttu-id="5407a-177">**Geen**: Hiermee geeft u de virtuele machine staat niet toe dat TLS-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="5407a-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="5407a-178">**Automatisch genereren**: de vereiste instellingen automatisch maakt voor het verbinding maken via TLS.</span><span class="sxs-lookup"><span data-stu-id="5407a-178">**Auto-generate**: Automatically creates the requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="5407a-179">**Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen TLS-instellingen.</span><span class="sxs-lookup"><span data-stu-id="5407a-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="5407a-180">Meer specifiek, moet de map de volgende zes bestanden bevatten:</span><span class="sxs-lookup"><span data-stu-id="5407a-180">More specifically, the directory must contain the following six files:</span></span>
                * <span data-ttu-id="5407a-181">*CA.PEM* en *ca key.pem*: het certificaat en openbare sleutel voor de TLS-certificeringsinstantie bevatten.</span><span class="sxs-lookup"><span data-stu-id="5407a-181">*ca.pem* and *ca-key.pem*: Contain the certificate and public key for the TLS Certificate Authority.</span></span>
                * <span data-ttu-id="5407a-182">*CERT.PEM* en *key.pem*: de client-certificaat en openbare sleutel die wordt gebruikt voor het TLS-verificatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="5407a-182">*cert.pem* and *key.pem*: Contain the client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="5407a-183">*Server.PEM* en *server key.pem*: het servercertificaat en de openbare sleutel voor de host bevatten.</span><span class="sxs-lookup"><span data-stu-id="5407a-183">*server.pem* and *server-key.pem*: Contain the server certificate and public key for the host.</span></span>

        ![Docker-Host maken][PUB06]

7. <span data-ttu-id="5407a-185">Nadat u alle voorgaande informatie hebt ingevoerd, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5407a-185">After you have entered all of the preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="5407a-186">In de **Docker-Container in Azure implementeren** wizard, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="5407a-186">In the **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![De Docker-Container implementeren in de Azure-wizard][PUB07]

9. <span data-ttu-id="5407a-188">In de **configureren de Docker-container gemaakt** venster de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="5407a-188">In the **Configure the Docker container to be created** window, do the following:</span></span>

   <span data-ttu-id="5407a-189">a.</span><span class="sxs-lookup"><span data-stu-id="5407a-189">a.</span></span> <span data-ttu-id="5407a-190">In de **Docker-containernaam** Voer een unieke naam voor uw Docker-container.</span><span class="sxs-lookup"><span data-stu-id="5407a-190">In the **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="5407a-191">b.</span><span class="sxs-lookup"><span data-stu-id="5407a-191">b.</span></span> <span data-ttu-id="5407a-192">Kies een van de volgende Docker-afbeeldingen:</span><span class="sxs-lookup"><span data-stu-id="5407a-192">Choose one of the following Docker images:</span></span>
     * <span data-ttu-id="5407a-193">**De installatiekopie van een vooraf gedefinieerde Docker**: Hiermee geeft u een bestaande Docker-installatiekopie uit Azure.</span><span class="sxs-lookup"><span data-stu-id="5407a-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="5407a-194">De lijst met Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die de Azure-Toolkit is geconfigureerd voor het patch zodat uw artefacten automatisch wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="5407a-194">The list of Docker images in this box consists of several images that the Azure Toolkit has been configured to patch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="5407a-195">**Aangepaste Dockerfile**: Hiermee geeft u een eerder opgeslagen Dockerfile vanaf uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="5407a-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="5407a-196">Dit is een geavanceerde functie voor ontwikkelaars die willen hun eigen Dockerfile implementeren.</span><span class="sxs-lookup"><span data-stu-id="5407a-196">This is a more advanced feature for developers who want to deploy their own Dockerfile.</span></span> <span data-ttu-id="5407a-197">Het is echter maximaal ontwikkelaars die gebruikmaken van deze optie om ervoor te zorgen dat hun Dockerfile correct is gebouwd.</span><span class="sxs-lookup"><span data-stu-id="5407a-197">However, it is up to developers who use this option to ensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="5407a-198">De Azure-Toolkit wordt de inhoud van een aangepaste Dockerfile niet gevalideerd, zodat de implementatie mislukken kan als de Dockerfile problemen heeft.</span><span class="sxs-lookup"><span data-stu-id="5407a-198">The Azure Toolkit does not validate the content in a custom Dockerfile, so the deployment might fail if the Dockerfile has issues.</span></span> <span data-ttu-id="5407a-199">Bovendien de Toolkit Azure verwacht de aangepaste Dockerfile bevatten een web-app-artefacten en wordt geprobeerd om een HTTP-verbinding te openen.</span><span class="sxs-lookup"><span data-stu-id="5407a-199">In addition, the Azure Toolkit expects the custom Dockerfile to contain a web app artifact, and it will attempt to open an HTTP connection.</span></span> <span data-ttu-id="5407a-200">Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="5407a-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="5407a-201">c.</span><span class="sxs-lookup"><span data-stu-id="5407a-201">c.</span></span> <span data-ttu-id="5407a-202">**Poortinstellingen**: Voer de unieke TCP-poort-binding voor de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="5407a-202">**Port settings**: Enter the unique TCP port binding for your Docker container.</span></span>

     ![Het configureren van de Docker-container venster worden gemaakt][PUB08]

10. <span data-ttu-id="5407a-204">Nadat u alle voorgaande stappen hebt voltooid, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="5407a-204">After you have completed all of the preceding steps, click **Finish**.</span></span>

<span data-ttu-id="5407a-205">De Toolkit Azure begint uw web-app implementeren naar Azure in een Docker-container.</span><span class="sxs-lookup"><span data-stu-id="5407a-205">The Azure Toolkit begins deploying your web app to Azure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5407a-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5407a-206">Next steps</span></span>
<span data-ttu-id="5407a-207">Zie de volgende bronnen voor meer informatie over de Azure-Toolkits voor IDE voor Java:</span><span class="sxs-lookup"><span data-stu-id="5407a-207">For more information about the Azure Toolkits for Java IDEs, see the following resources:</span></span>

* <span data-ttu-id="5407a-208">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5407a-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5407a-209">[Wat is er nieuw in de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5407a-209">[What's new in the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5407a-210">[Installing the Azure Toolkit for Eclipse] (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="5407a-210">[Installing the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5407a-211">[Aanmelden instructies voor de Azure-werkset voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5407a-211">[Sign-in instructions for the Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="5407a-212">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="5407a-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="5407a-213">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5407a-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5407a-214">[Wat is er nieuw in de Azure-werkset voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5407a-214">[What's new in the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5407a-215">[Installing the Azure Toolkit for IntelliJ] (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="5407a-215">[Installing the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5407a-216">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5407a-216">[Sign-in instructions for the Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="5407a-217">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="5407a-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="5407a-218">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="5407a-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="5407a-219">Zie voor aanvullende bronnen voor Docker de officiële [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="5407a-219">For additional resources for Docker, see the official [Docker website].</span></span>

<!-- URL List -->

<span data-ttu-id="5407a-220">[Azure Toolkit voor Eclipse]: ./azure-toolkit-for-eclipse.md</span><span class="sxs-lookup"><span data-stu-id="5407a-220">[Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse.md</span></span>
<span data-ttu-id="5407a-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="5407a-221">[Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij.md</span></span>
<span data-ttu-id="5407a-222">[Een Hallo wereld-web-app maken voor Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="5407a-222">[Create a Hello World web app for Azure in Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md</span></span>
<span data-ttu-id="5407a-223">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span><span class="sxs-lookup"><span data-stu-id="5407a-223">[Create a Hello World web app for Azure in IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md</span></span>
<span data-ttu-id="5407a-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md (De Azure Toolkit voor Eclipse installeren)</span><span class="sxs-lookup"><span data-stu-id="5407a-224">[Installing the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-installation.md</span></span>
<span data-ttu-id="5407a-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md (De Azure Toolkit voor IntelliJ installeren)</span><span class="sxs-lookup"><span data-stu-id="5407a-225">[Installing the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-installation.md</span></span>
<span data-ttu-id="5407a-226">[Aanmelden instructies voor de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="5407a-226">[Sign-in instructions for the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md</span></span>
<span data-ttu-id="5407a-227">[Aanmelden instructies voor de Azure-Toolkit voor IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span><span class="sxs-lookup"><span data-stu-id="5407a-227">[Sign-in instructions for the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md</span></span>
<span data-ttu-id="5407a-228">[Wat is er nieuw in de Azure-werkset voor Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="5407a-228">[What's new in the Azure Toolkit for Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md</span></span>
<span data-ttu-id="5407a-229">[Wat is er nieuw in de Azure-werkset voor IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span><span class="sxs-lookup"><span data-stu-id="5407a-229">[What's new in the Azure Toolkit for IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md</span></span>

<span data-ttu-id="5407a-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="5407a-230">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
<span data-ttu-id="5407a-231">[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="5407a-231">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>

<span data-ttu-id="5407a-232">[Docker-website]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="5407a-232">[Docker website]: https://www.docker.com/</span></span>

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png