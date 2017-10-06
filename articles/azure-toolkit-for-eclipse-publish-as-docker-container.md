---
title: aaaPublish een Docker-container met behulp van Azure Toolkit voor Eclipse Hallo | Microsoft Docs
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
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a><span data-ttu-id="ef448-103">Een web-app publiceren als een Docker-container met behulp van hello Azure Toolkit voor Eclipse</span><span class="sxs-lookup"><span data-stu-id="ef448-103">Publish a web app as a Docker container by using hello Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="ef448-104">Docker-containers zijn een veelgebruikte methode voor het implementeren van webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="ef448-104">Docker containers are a widely used method for deploying web applications.</span></span> <span data-ttu-id="ef448-105">Met behulp van Docker-containers kunnen ontwikkelaars alle projectbestanden en afhankelijkheden in een enkel pakket voor tooa implementatieserver consolideren.</span><span class="sxs-lookup"><span data-stu-id="ef448-105">By using Docker containers, developers can consolidate all their project files and dependencies into a single package for deployment tooa server.</span></span> <span data-ttu-id="ef448-106">Hello Azure Toolkit voor Eclipse vereenvoudigt dit proces voor Java-ontwikkelaars door toe te voegen *publiceren als Docker-Container* functies voor implementatie tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ef448-106">hello Azure Toolkit for Eclipse simplifies this process for Java developers by adding *Publish as Docker Container* features for deployment tooMicrosoft Azure.</span></span> <span data-ttu-id="ef448-107">Dit artikel begeleidt u bij Hallo stappen vereist toopublish uw toepassingen tooAzure als Docker-containers.</span><span class="sxs-lookup"><span data-stu-id="ef448-107">This article walks you through hello steps required toopublish your applications tooAzure as Docker containers.</span></span>

> [!NOTE]
> <span data-ttu-id="ef448-108">Meer informatie over Docker is beschikbaar op Hallo [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="ef448-108">More information about Docker is available on hello [Docker website].</span></span>
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a><span data-ttu-id="ef448-109">Uw web-app tooAzure publiceren met behulp van Docker-container</span><span class="sxs-lookup"><span data-stu-id="ef448-109">Publish your web app tooAzure by using a Docker container</span></span>

1. <span data-ttu-id="ef448-110">Open uw web-app-project in Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ef448-110">Open your web app project in Eclipse.</span></span>

2. <span data-ttu-id="ef448-111">Hallo toostart **publiceren als Docker-Container** wizard Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="ef448-111">toostart hello **Publish as Docker Container** wizard, do either of hello following:</span></span>

   * <span data-ttu-id="ef448-112">In Hallo **Navigator** weergeven, met de rechtermuisknop op uw project, klik op **Azure**, en klik vervolgens op **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="ef448-112">In hello **Navigator** view, right-click your project, click **Azure**, and then click **Publish as Docker Container**.</span></span>

      ![Weergave van de Navigator publiceren als de opdracht Docker-Container][PUB01]

   * <span data-ttu-id="ef448-114">Klik op Hallo Eclipse werkbalk op Hallo **publiceren** knop en klik vervolgens op **publiceren als Docker-Container**.</span><span class="sxs-lookup"><span data-stu-id="ef448-114">On hello Eclipse toolbar, click hello **Publish** button, and then click **Publish as Docker Container**.</span></span>

      ![Werkbalk van eclipse publiceren als de opdracht Docker-Container][PUB02]
      
    <span data-ttu-id="ef448-116">Hallo **Docker-Container in Azure implementeren** wizard wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="ef448-116">hello **Deploy Docker Container on Azure** wizard opens.</span></span>

    ![Hallo Docker-Container in de wizard Azure implementeren][PUB03]

3. <span data-ttu-id="ef448-118">In Hallo **typt u een installatiekopie met de naam, selecteer Hallo-artefact pad en controleren van een Docker host toobe gebruikt** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef448-118">In hello **Type an image name, select hello artifact's path and check a Docker host toobe used** window, do hello following:</span></span>

    <span data-ttu-id="ef448-119">a.</span><span class="sxs-lookup"><span data-stu-id="ef448-119">a.</span></span> <span data-ttu-id="ef448-120">In Hallo **Docker installatiekopienaam** Voer een unieke naam voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="ef448-120">In hello **Docker image name** box, enter a unique name for your Docker host.</span></span> <span data-ttu-id="ef448-121">(Hallo wizard maakt automatisch een naam, maar u kunt deze wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="ef448-121">(hello wizard automatically creates a name, but you can modify it.)</span></span>

    <span data-ttu-id="ef448-122">b.</span><span class="sxs-lookup"><span data-stu-id="ef448-122">b.</span></span> <span data-ttu-id="ef448-123">Hallo **Hosts** gebied worden weergegeven voor alle Docker-hosts die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef448-123">hello **Hosts** area displays any Docker hosts that you have already created.</span></span> <span data-ttu-id="ef448-124">Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="ef448-124">Do either of hello following:</span></span>

    * <span data-ttu-id="ef448-125">Als u een bestaande Docker-host hebt, kunt u uw web-app tooit kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="ef448-125">If you have an existing Docker host, you can deploy your web app tooit.</span></span>
    * <span data-ttu-id="ef448-126">toocreate een nieuwe Docker-host, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ef448-126">toocreate a new Docker host, click **Add**.</span></span>  
      
    <span data-ttu-id="ef448-127">Hallo **Docker-Host maken** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="ef448-127">hello **Create Docker Host** dialog box opens.</span></span>

    ![Docker-Container in de Wizard Azure implementeren][PUB04a]

4. <span data-ttu-id="ef448-129">In Hallo **Hallo nieuwe virtuele machine configureren** venster Hallo volgend opties voor de Docker-host opgeeft.</span><span class="sxs-lookup"><span data-stu-id="ef448-129">In hello **Configure hello new virtual machine** window, specify hello following options for your Docker host.</span></span> <span data-ttu-id="ef448-130">(Hallo wizard genereert automatisch Hallo opties waarmee u de meeste, maar u deze kunt wijzigen.)</span><span class="sxs-lookup"><span data-stu-id="ef448-130">(hello wizard automatically generates most of hello options for you, but you can modify any of them.)</span></span>

   <span data-ttu-id="ef448-131">a.</span><span class="sxs-lookup"><span data-stu-id="ef448-131">a.</span></span> <span data-ttu-id="ef448-132">**Naam**: Voer een unieke naam voor Hallo Docker-host.</span><span class="sxs-lookup"><span data-stu-id="ef448-132">**Name**: Enter a unique name for hello Docker host.</span></span> <span data-ttu-id="ef448-133">(Dit is hetzelfde als de naam van de Docker-installatiekopie die u eerder hebt opgegeven Hallo niet Hallo.)</span><span class="sxs-lookup"><span data-stu-id="ef448-133">(It is not hello same as hello Docker image name that you specified earlier.)</span></span>

   <span data-ttu-id="ef448-134">b.</span><span class="sxs-lookup"><span data-stu-id="ef448-134">b.</span></span> <span data-ttu-id="ef448-135">**Abonnement**: Voer hello Azure-abonnement dat u voor de host gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ef448-135">**Subscription**: Enter hello Azure subscription that you use for your host.</span></span>

   <span data-ttu-id="ef448-136">c.</span><span class="sxs-lookup"><span data-stu-id="ef448-136">c.</span></span> <span data-ttu-id="ef448-137">**Regio**: Voer Hallo geografische regio waar uw host bevindt.</span><span class="sxs-lookup"><span data-stu-id="ef448-137">**Region**: Enter hello geographical region where your host is located.</span></span>

   <span data-ttu-id="ef448-138">d.</span><span class="sxs-lookup"><span data-stu-id="ef448-138">d.</span></span> <span data-ttu-id="ef448-139">Op Hallo **Host-OS en de grootte** tabblad:</span><span class="sxs-lookup"><span data-stu-id="ef448-139">On hello **Host OS and Size** tab:</span></span>
     * <span data-ttu-id="ef448-140">**Host-OS**: Voer Hallo-besturingssysteem voor Hallo virtuele machine met de host.</span><span class="sxs-lookup"><span data-stu-id="ef448-140">**Host OS**: Enter hello operating system for hello virtual machine that contains your host.</span></span>
     * <span data-ttu-id="ef448-141">**De grootte van**: Geef de grootte voor de virtuele machine Hallo voor de host.</span><span class="sxs-lookup"><span data-stu-id="ef448-141">**Size**: Enter hello virtual-machine size for your host.</span></span>

   <span data-ttu-id="ef448-142">e.</span><span class="sxs-lookup"><span data-stu-id="ef448-142">e.</span></span> <span data-ttu-id="ef448-143">Op Hallo **resourcegroep** tabblad:</span><span class="sxs-lookup"><span data-stu-id="ef448-143">On hello **Resource Group** tab:</span></span>
     * <span data-ttu-id="ef448-144">**Nieuwe resourcegroep**: een nieuwe resourcegroep maken voor de host.</span><span class="sxs-lookup"><span data-stu-id="ef448-144">**New resource group**: Create a new resource group for your host.</span></span>
     * <span data-ttu-id="ef448-145">**Bestaande resourcegroep**: Voer een bestaande resourcegroep van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ef448-145">**Existing resource group**: Enter an existing resource group from your Azure account.</span></span>

   <span data-ttu-id="ef448-146">f.</span><span class="sxs-lookup"><span data-stu-id="ef448-146">f.</span></span> <span data-ttu-id="ef448-147">Op Hallo **netwerk** tabblad:</span><span class="sxs-lookup"><span data-stu-id="ef448-147">On hello **Network** tab:</span></span>
     * <span data-ttu-id="ef448-148">**Nieuw virtueel netwerk**: Maak een nieuw virtueel netwerk voor de host.</span><span class="sxs-lookup"><span data-stu-id="ef448-148">**New virtual network**: Create a new virtual network for your host.</span></span>
     * <span data-ttu-id="ef448-149">**Bestaand virtueel netwerk**: Voer een bestaand virtueel netwerk van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ef448-149">**Existing virtual network**: Enter an existing virtual network from your Azure account.</span></span>

   <span data-ttu-id="ef448-150">g.</span><span class="sxs-lookup"><span data-stu-id="ef448-150">g.</span></span> <span data-ttu-id="ef448-151">Op Hallo **opslag** tabblad:</span><span class="sxs-lookup"><span data-stu-id="ef448-151">On hello **Storage** tab:</span></span>
     * <span data-ttu-id="ef448-152">**Nieuw opslagaccount**: Maak een nieuw opslagaccount voor de host.</span><span class="sxs-lookup"><span data-stu-id="ef448-152">**New storage account**: Create a new storage account for your host.</span></span>
     * <span data-ttu-id="ef448-153">**Bestaande opslagaccount**: Voer een bestaand opslagaccount van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ef448-153">**Existing storage account**: Enter an existing storage account from your Azure account.</span></span>

5. <span data-ttu-id="ef448-154">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="ef448-154">Click **Next**.</span></span>

6. <span data-ttu-id="ef448-155">In Hallo **logboek referenties configureren en poortinstellingen** venster, selecteert u een van de Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="ef448-155">In hello **Configure log in credentials and port settings** window, select one of hello following options:</span></span>

    * <span data-ttu-id="ef448-156">**Referenties importeren uit Azure Key Vault**: Hiermee geeft u een eerder opgeslagen set referenties die zijn opgeslagen in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ef448-156">**Import credentials from Azure Key Vault**: Specifies a previously saved set of credentials that are stored in your Azure subscription.</span></span>

      >[!NOTE]
      ><span data-ttu-id="ef448-157">Een Azure Key Vault dat gemaakt met een specifiek account of een service-principal is niet automatisch toegankelijk is door een ander account of service-principal die Hallo-abonnement deelt.</span><span class="sxs-lookup"><span data-stu-id="ef448-157">An Azure Key Vault that's created with a specific account or service principal is not automatically accessible by another account or service principal that shares hello subscription.</span></span> <span data-ttu-id="ef448-158">tooallow een ander account of de service principal toouse Hallo Sleutelkluis, moet u hello Azure portal tooadd Hallo account of service-principal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef448-158">tooallow another account or service principal toouse hello Key Vault, you must use hello Azure portal tooadd hello account or service principal.</span></span>

    * <span data-ttu-id="ef448-159">**Nieuwe aanmelding referenties**: maakt een nieuwe set aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="ef448-159">**New log in credentials**: Creates a new set of login credentials.</span></span> <span data-ttu-id="ef448-160">Als u deze optie selecteert, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef448-160">If you select this option, do hello following:</span></span>
    
      * <span data-ttu-id="ef448-161">Op Hallo **VM referenties** tabblad, kiest u een van de volgende Hallo opties voor Hallo virtuele machines-aanmeldingsreferenties van de Docker-host:</span><span class="sxs-lookup"><span data-stu-id="ef448-161">On hello **VM Credentials** tab, choose one of hello following options for hello virtual-machine login credentials of your Docker host:</span></span>

          * <span data-ttu-id="ef448-162">**Gebruikersnaam**: Hallo gebruikersnaam invoeren voor de aanmeldingsreferenties van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ef448-162">**Username**: Enter hello username for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="ef448-163">**Wachtwoord** en **bevestigen**: Hallo wachtwoord invoeren voor de aanmeldingsreferenties van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ef448-163">**Password** and **Confirm**: Enter hello password for your virtual machine login credentials.</span></span>
          * <span data-ttu-id="ef448-164">**SSH**: Voer Hallo Secure Shell (SSH)-instellingen voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="ef448-164">**SSH**: Enter hello Secure Shell (SSH) settings for your Docker host.</span></span> <span data-ttu-id="ef448-165">U kunt kiezen uit Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="ef448-165">You can choose from hello following options:</span></span>
            * <span data-ttu-id="ef448-166">**Geen**: Hiermee geeft u de virtuele machine staat niet toe dat SSH-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ef448-166">**None**: Specifies that your virtual machine will not allow SSH connections.</span></span>
            * <span data-ttu-id="ef448-167">**Automatisch genereren**: automatisch maakt Hallo vereiste instellingen voor verbinding maken via SSH.</span><span class="sxs-lookup"><span data-stu-id="ef448-167">**Auto-generate**: Automatically creates hello requisite settings for connecting via SSH.</span></span>
            * <span data-ttu-id="ef448-168">**Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen SSH-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ef448-168">**Import from directory**: Specifies a directory that contains a set of previously saved SSH settings.</span></span> <span data-ttu-id="ef448-169">Hallo directory moet de volgende twee bestanden Hallo bevatten:</span><span class="sxs-lookup"><span data-stu-id="ef448-169">hello directory must contain hello following two files:</span></span>
                * <span data-ttu-id="ef448-170">*id_rsa*: Hallo RSA-id voor een gebruiker bevat.</span><span class="sxs-lookup"><span data-stu-id="ef448-170">*id_rsa*: Contains hello RSA identification for a user.</span></span>
                * <span data-ttu-id="ef448-171">*id_rsa.pub*: bevat Hallo openbare RSA-sleutel die wordt gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="ef448-171">*id_rsa.pub*: Contains hello RSA public key that is used for authentication.</span></span>
        
        ![Docker-Host maken][PUB05]

      * <span data-ttu-id="ef448-173">Op Hallo **Docker-Daemon referenties** tabblad, Hallo volgende opties opgeven:</span><span class="sxs-lookup"><span data-stu-id="ef448-173">On hello **Docker Daemon Credentials** tab, specify hello following options:</span></span>

          * <span data-ttu-id="ef448-174">**Docker-Daemon poort**: Voer Hallo unieke TCP-poort voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="ef448-174">**Docker Daemon port**: Enter hello unique TCP port for your Docker host.</span></span>
          * <span data-ttu-id="ef448-175">**TLS beveiliging**: Voer Hallo Transport Layer Security-instellingen voor de Docker-host.</span><span class="sxs-lookup"><span data-stu-id="ef448-175">**TLS Security**: Enter hello Transport Layer Security settings for your Docker host.</span></span> <span data-ttu-id="ef448-176">U kunt kiezen uit Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="ef448-176">You can choose from hello following options:</span></span>
            * <span data-ttu-id="ef448-177">**Geen**: Hiermee geeft u de virtuele machine staat niet toe dat TLS-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="ef448-177">**None**: Specifies that your virtual machine will not allow TLS connections.</span></span>
            * <span data-ttu-id="ef448-178">**Automatisch genereren**: automatisch maakt Hallo vereiste instellingen voor verbinding maken via TLS.</span><span class="sxs-lookup"><span data-stu-id="ef448-178">**Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.</span></span>
            * <span data-ttu-id="ef448-179">**Importeren uit directory**: Hiermee geeft u een map met een set van de eerder opgeslagen TLS-instellingen.</span><span class="sxs-lookup"><span data-stu-id="ef448-179">**Import from directory**: Specifies a directory that contains a set of previously saved TLS settings.</span></span> <span data-ttu-id="ef448-180">Hallo directory moet meer specifiek, Hallo volgende zes bestanden bevatten:</span><span class="sxs-lookup"><span data-stu-id="ef448-180">More specifically, hello directory must contain hello following six files:</span></span>
                * <span data-ttu-id="ef448-181">*CA.PEM* en *ca key.pem*: Hallo-certificaat en openbare sleutel voor Hallo TLS certificeringsinstantie bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef448-181">*ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.</span></span>
                * <span data-ttu-id="ef448-182">*CERT.PEM* en *key.pem*: Hallo-clientcertificaat en openbare sleutel die wordt gebruikt voor het TLS-verificatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef448-182">*cert.pem* and *key.pem*: Contain hello client certificate and public key that is used for TLS authentication.</span></span>
                * <span data-ttu-id="ef448-183">*Server.PEM* en *server key.pem*: Hallo servercertificaat en openbare sleutel voor Hallo host bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef448-183">*server.pem* and *server-key.pem*: Contain hello server certificate and public key for hello host.</span></span>

        ![Docker-Host maken][PUB06]

7. <span data-ttu-id="ef448-185">Nadat u alle voorgaande informatie Hallo hebt ingevoerd, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="ef448-185">After you have entered all of hello preceding information, click **Finish**.</span></span>

8. <span data-ttu-id="ef448-186">In Hallo **Docker-Container in Azure implementeren** wizard, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ef448-186">In hello **Deploy Docker Container on Azure** wizard, click **Next**.</span></span>

   ![Hallo Docker-Container in de wizard Azure implementeren][PUB07]

9. <span data-ttu-id="ef448-188">In Hallo **hello Docker-container toobe gemaakt configureren** venster Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef448-188">In hello **Configure hello Docker container toobe created** window, do hello following:</span></span>

   <span data-ttu-id="ef448-189">a.</span><span class="sxs-lookup"><span data-stu-id="ef448-189">a.</span></span> <span data-ttu-id="ef448-190">In Hallo **Docker-containernaam** Voer een unieke naam voor uw Docker-container.</span><span class="sxs-lookup"><span data-stu-id="ef448-190">In hello **Docker container name** box, enter a unique name for your Docker container.</span></span>

   <span data-ttu-id="ef448-191">b.</span><span class="sxs-lookup"><span data-stu-id="ef448-191">b.</span></span> <span data-ttu-id="ef448-192">Kies een van de Hallo Docker-installatiekopieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef448-192">Choose one of hello following Docker images:</span></span>
     * <span data-ttu-id="ef448-193">**De installatiekopie van een vooraf gedefinieerde Docker**: Hiermee geeft u een bestaande Docker-installatiekopie uit Azure.</span><span class="sxs-lookup"><span data-stu-id="ef448-193">**Predefined Docker image**: Specifies a pre-existing Docker image from Azure.</span></span>

       >[!NOTE]
       ><span data-ttu-id="ef448-194">Hallo-lijst van Docker-afbeeldingen in dit vak bestaat uit diverse installatiekopieën die Azure Toolkit is Hallo toopatch zo geconfigureerd dat uw artefacten automatisch wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ef448-194">hello list of Docker images in this box consists of several images that hello Azure Toolkit has been configured toopatch so that your artifact is deployed automatically.</span></span>

     * <span data-ttu-id="ef448-195">**Aangepaste Dockerfile**: Hiermee geeft u een eerder opgeslagen Dockerfile vanaf uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="ef448-195">**Custom Dockerfile**: Specifies a previously saved Dockerfile from your local computer.</span></span>

       >[!NOTE]
       ><span data-ttu-id="ef448-196">Dit is een geavanceerde functie voor ontwikkelaars die toodeploy hun eigen Dockerfile willen.</span><span class="sxs-lookup"><span data-stu-id="ef448-196">This is a more advanced feature for developers who want toodeploy their own Dockerfile.</span></span> <span data-ttu-id="ef448-197">Het is echter van toodevelopers die gebruikmaken van deze optie tooensure die hun Dockerfile correct is ingebouwd.</span><span class="sxs-lookup"><span data-stu-id="ef448-197">However, it is up toodevelopers who use this option tooensure that their Dockerfile is built correctly.</span></span> <span data-ttu-id="ef448-198">Hello Azure Toolkit valideren Hallo inhoud in een aangepaste Dockerfile zodat het Hallo-implementatie kan mislukken als Hallo Dockerfile problemen heeft.</span><span class="sxs-lookup"><span data-stu-id="ef448-198">hello Azure Toolkit does not validate hello content in a custom Dockerfile, so hello deployment might fail if hello Dockerfile has issues.</span></span> <span data-ttu-id="ef448-199">Bovendien hello Azure Toolkit verwacht Hallo aangepaste Dockerfile toocontain een artefact van web-app en wordt geprobeerd tooopen een HTTP-verbinding.</span><span class="sxs-lookup"><span data-stu-id="ef448-199">In addition, hello Azure Toolkit expects hello custom Dockerfile toocontain a web app artifact, and it will attempt tooopen an HTTP connection.</span></span> <span data-ttu-id="ef448-200">Als ontwikkelaars een ander type artefact publiceert, krijgen ze mogelijk onschuldig fouten na de implementatie.</span><span class="sxs-lookup"><span data-stu-id="ef448-200">If developers publish a different type of artifact, they may receive innocuous errors after deployment.</span></span>

   <span data-ttu-id="ef448-201">c.</span><span class="sxs-lookup"><span data-stu-id="ef448-201">c.</span></span> <span data-ttu-id="ef448-202">**Poortinstellingen**: Voer Hallo unieke TCP-poortbinding voor de Docker-container.</span><span class="sxs-lookup"><span data-stu-id="ef448-202">**Port settings**: Enter hello unique TCP port binding for your Docker container.</span></span>

     ![Hallo configureren Hallo Docker-container gemaakt toobe venster][PUB08]

10. <span data-ttu-id="ef448-204">Nadat u alle Hallo vorige stappen hebt voltooid, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="ef448-204">After you have completed all of hello preceding steps, click **Finish**.</span></span>

<span data-ttu-id="ef448-205">Hello Azure Toolkit begint de tooAzure van uw web-app in een Docker-container te implementeren.</span><span class="sxs-lookup"><span data-stu-id="ef448-205">hello Azure Toolkit begins deploying your web app tooAzure in a Docker container.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ef448-206">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef448-206">Next steps</span></span>
<span data-ttu-id="ef448-207">Zie voor meer informatie over hello Azure Toolkits voor IDE voor Java Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef448-207">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="ef448-208">[Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef448-208">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ef448-209">[Wat is er nieuw in hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef448-209">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ef448-210">[Hello Azure Toolkit voor Eclipse installeren]</span><span class="sxs-lookup"><span data-stu-id="ef448-210">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ef448-211">[Aanmelden instructies voor het hello Azure Toolkit voor Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef448-211">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="ef448-212">[Een Hallo wereld-web-app maken voor Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="ef448-212">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="ef448-213">[Azure Toolkit for IntelliJ] (Azure Toolkit voor IntelliJ)</span><span class="sxs-lookup"><span data-stu-id="ef448-213">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ef448-214">[Wat is er nieuw in hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ef448-214">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ef448-215">[Hello Azure Toolkit voor IntelliJ installeren]</span><span class="sxs-lookup"><span data-stu-id="ef448-215">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ef448-216">[Aanmelden instructies voor hello Azure Toolkit voor IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ef448-216">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="ef448-217">[Een Hallo wereld-web-app maken voor Azure in IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="ef448-217">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="ef448-218">Zie voor meer informatie over het gebruik van Azure met Java [Azure Java Developer Center] en [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="ef448-218">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="ef448-219">Zie voor aanvullende bronnen voor Docker Hallo officiële [Docker-website].</span><span class="sxs-lookup"><span data-stu-id="ef448-219">For additional resources for Docker, see hello official [Docker website].</span></span>

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