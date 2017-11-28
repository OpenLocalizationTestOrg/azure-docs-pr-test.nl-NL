---
title: een App Spring opstarten op Kubernetes in Azure Container Service aaaDeploy | Microsoft Docs
description: Deze zelfstudie leert u echter Hallo stappen toodeploy een versie die voorjaar Boot-toepassing in een cluster Kubernetes op Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a><span data-ttu-id="dff7d-103">Een toepassing Spring opstarten op een Kubernetes Cluster in hello Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="dff7d-103">Deploy a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>

<span data-ttu-id="dff7d-104">Hallo  **[Spring Framework]**  is een populaire open-source framework waarmee ontwikkelaars van Java web, mobiel en API-toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="dff7d-104">hello **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="dff7d-105">In deze zelfstudie wordt een voorbeeld-app gemaakt met behulp van [Spring Boot], een conventie voor gestuurde benadering voor het gebruik van Spring tooget snel aan de slag.</span><span class="sxs-lookup"><span data-stu-id="dff7d-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring tooget started quickly.</span></span>

<span data-ttu-id="dff7d-106">**[Kubernetes]**  en  **[Docker]**  zijn open source-oplossingen die ontwikkelaars helpen bij automatiseren Hallo-implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd in de containers.</span><span class="sxs-lookup"><span data-stu-id="dff7d-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate hello deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="dff7d-107">Deze zelfstudie helpt u al deze twee populaire open-source technologieën toodevelop combineren en implementeren van een versie die voorjaar opstarten toepassing tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="dff7d-107">This tutorial walks you though combining these two popular, open-source technologies toodevelop and deploy a Spring Boot application tooMicrosoft Azure.</span></span> <span data-ttu-id="dff7d-108">Meer specifiek, gebruikt u  *[Spring Boot]*  voor toepassingsontwikkeling,  *[Kubernetes]*  voor implementatie van de container en Hallo [Azure Container Service (ACS)] toohost uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="dff7d-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and hello [Azure Container Service (ACS)] toohost your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="dff7d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dff7d-109">Prerequisites</span></span>

* <span data-ttu-id="dff7d-110">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="dff7d-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="dff7d-111">Hallo [Azure-opdrachtregelinterface (CLI)].</span><span class="sxs-lookup"><span data-stu-id="dff7d-111">hello [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="dff7d-112">Een up-to-date [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="dff7d-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="dff7d-113">Apache van [Maven] bouwen tool (versie 3).</span><span class="sxs-lookup"><span data-stu-id="dff7d-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="dff7d-114">Een [Git] client.</span><span class="sxs-lookup"><span data-stu-id="dff7d-114">A [Git] client.</span></span>
* <span data-ttu-id="dff7d-115">Een [Docker] client.</span><span class="sxs-lookup"><span data-stu-id="dff7d-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="dff7d-116">Vanwege toohello virtualisatie vereisten van deze zelfstudie, kan niet u Hallo stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="dff7d-116">Due toohello virtualization requirements of this tutorial, you cannot follow hello steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="dff7d-117">Hallo Spring opstarten op Docker aan de slag web-app maken</span><span class="sxs-lookup"><span data-stu-id="dff7d-117">Create hello Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="dff7d-118">Hallo stappen te volgen helpt u bij het bouwen van een webtoepassing Spring opstarten en lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="dff7d-118">hello following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="dff7d-119">Open een opdrachtprompt en maken van een lokale map toohold uw toepassing en de wijziging toothat directory; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dff7d-119">Open a command-prompt and create a local directory toohold your application, and change toothat directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="dff7d-120">-- of--</span><span class="sxs-lookup"><span data-stu-id="dff7d-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="dff7d-121">Kloon Hallo [Spring opstarten op het Docker aan de slag] voorbeeldproject in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="dff7d-121">Clone hello [Spring Boot on Docker Getting Started] sample project into hello directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="dff7d-122">Wijzig de directory toohello voltooid project.</span><span class="sxs-lookup"><span data-stu-id="dff7d-122">Change directory toohello completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="dff7d-123">Maven toobuild en Voer Hallo voorbeeld-app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dff7d-123">Use Maven toobuild and run hello sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="dff7d-124">Test Hallo web-app door te bladeren toohttp://localhost:8080 of door de volgende Hallo `curl` opdracht:</span><span class="sxs-lookup"><span data-stu-id="dff7d-124">Test hello web app by browsing toohttp://localhost:8080, or with hello following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="dff7d-125">U ziet Hallo volgende bericht wordt weergegeven: **Hallo Docker wereld**</span><span class="sxs-lookup"><span data-stu-id="dff7d-125">You should see hello following message displayed: **Hello Docker World**</span></span>

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a><span data-ttu-id="dff7d-127">Maken van een Azure Container Registry hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="dff7d-127">Create an Azure Container Registry using hello Azure CLI</span></span>

1. <span data-ttu-id="dff7d-128">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="dff7d-128">Open a command prompt.</span></span>

1. <span data-ttu-id="dff7d-129">Meld u bij tooyour Azure-account:</span><span class="sxs-lookup"><span data-stu-id="dff7d-129">Log in tooyour Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="dff7d-130">Maak een resourcegroep voor hello Azure-resources in deze zelfstudie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dff7d-130">Create a resource group for hello Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="dff7d-131">Maak een register persoonlijke Azure-container in Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="dff7d-131">Create a private Azure container registry in hello resource group.</span></span> <span data-ttu-id="dff7d-132">Hallo-zelfstudie duwt Hallo voorbeeld-app als een Docker installatiekopie toothis register in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="dff7d-132">hello tutorial pushes hello sample app as a Docker image toothis registry in later steps.</span></span> <span data-ttu-id="dff7d-133">Vervang `wingtiptoysregistry` met een unieke naam voor het register.</span><span class="sxs-lookup"><span data-stu-id="dff7d-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a><span data-ttu-id="dff7d-134">Uw app toohello container register push</span><span class="sxs-lookup"><span data-stu-id="dff7d-134">Push your app toohello container registry</span></span>

1. <span data-ttu-id="dff7d-135">Navigeer toohello configuratiemap voor uw installatie Maven (standaard ~/.m2/ of C:\Users\username\.m2) en open Hallo *settings.xml* bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="dff7d-135">Navigate toohello configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open hello *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="dff7d-136">Hallo-wachtwoord voor uw register container ophalen met hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="dff7d-136">Retrieve hello password for your container registry from hello Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="dff7d-137">Toevoegen van uw Azure-Container register-id en wachtwoord tooa nieuwe `<server>` verzameling in hello *settings.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="dff7d-137">Add your Azure Container Registry id and password tooa new `<server>` collection in hello *settings.xml* file.</span></span>
<span data-ttu-id="dff7d-138">Hallo `id` en `username` Hallo-naam van het register Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="dff7d-138">hello `id` and `username` are hello name of hello registry.</span></span> <span data-ttu-id="dff7d-139">Gebruik Hallo `password` waarde uit de vorige opdracht hello (zonder aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="dff7d-139">Use hello `password` value from hello previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="dff7d-140">Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten (bijvoorbeeld '*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker / volledige*'), en open Hallo *pom.xml* bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="dff7d-140">Navigate toohello completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open hello *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="dff7d-141">Update Hallo `<properties>` verzameling in hello *pom.xml* -bestand met Hallo aanmelding serverwaarde voor uw Azure-Container-register.</span><span class="sxs-lookup"><span data-stu-id="dff7d-141">Update hello `<properties>` collection in hello *pom.xml* file with hello login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="dff7d-142">Update Hallo `<plugins>` verzameling in hello *pom.xml* bestand die Hallo `<plugin>` Hallo aanmelding adres en het register servernaam voor uw Azure-Container register bevat.</span><span class="sxs-lookup"><span data-stu-id="dff7d-142">Update hello `<plugins>` collection in hello *pom.xml* file so that hello `<plugin>` contains hello login server address and registry name for your Azure Container Registry.</span></span>

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. <span data-ttu-id="dff7d-143">Navigeer projectmap toohello voltooid voor uw toepassing Spring opstarten en Voer Hallo opdracht toobuild hello Docker-container en push Hallo installatiekopie toohello register te volgen:</span><span class="sxs-lookup"><span data-stu-id="dff7d-143">Navigate toohello completed project directory for your Spring Boot application and run hello following command toobuild hello Docker container and push hello image toohello registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="dff7d-144">Er wordt een foutbericht weergegeven dat vergelijkbaar tooone van de volgende Hallo is wanneer Maven pushes Hallo installatiekopie tooAzure:</span><span class="sxs-lookup"><span data-stu-id="dff7d-144">You may receive an error message that is similar tooone of hello following when Maven pushes hello image tooAzure:</span></span>
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="dff7d-145">Als u deze fout krijgt, meld u bij tooAzure vanaf Hallo Docker-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="dff7d-145">If you get this error, log in tooAzure from hello Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="dff7d-146">Vervolgens push uw container:</span><span class="sxs-lookup"><span data-stu-id="dff7d-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a><span data-ttu-id="dff7d-147">Maak een Kubernetes Cluster op ACS hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="dff7d-147">Create a Kubernetes Cluster on ACS using hello Azure CLI</span></span>

1. <span data-ttu-id="dff7d-148">Maak een Kubernetes-cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="dff7d-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="dff7d-149">Hallo volgende opdracht maakt u een *kubernetes* cluster in Hallo *wingtiptoys kubernetes* resource groep met *wingtiptoys containerservice* als Hallo-cluster naam, en *wingtiptoys kubernetes* als Hallo DNS-voorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="dff7d-149">hello following command creates a *kubernetes* cluster in hello *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as hello cluster name, and *wingtiptoys-kubernetes* as hello DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="dff7d-150">Met deze opdracht kan een tijdje duren toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dff7d-150">This command may take a while toocomplete.</span></span>

1. <span data-ttu-id="dff7d-151">Installeer `kubectl` met behulp van Azure CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="dff7d-151">Install `kubectl` using hello Azure CLI.</span></span> <span data-ttu-id="dff7d-152">Linux-gebruikers wellicht tooprefix deze opdracht met `sudo` omdat deze Hallo Kubernetes CLI te implementeert`/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="dff7d-152">Linux users may have tooprefix this command with `sudo` since it deploys hello Kubernetes CLI too`/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="dff7d-153">Downloaden van informatie over de configuratie van de Hallo cluster zodat u uw cluster vanuit de Hallo Kubernetes webinterface beheren kunt en `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="dff7d-153">Download hello cluster configuration information so you can manage your cluster from hello Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a><span data-ttu-id="dff7d-154">Hallo installatiekopie tooyour Kubernetes cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="dff7d-154">Deploy hello image tooyour Kubernetes cluster</span></span>

<span data-ttu-id="dff7d-155">Deze zelfstudie implementeert Hallo app met behulp `kubectl`, klikt u vervolgens kunt u tooexplore Hallo implementatie via Hallo Kubernetes webinterface.</span><span class="sxs-lookup"><span data-stu-id="dff7d-155">This tutorial deploys hello app using `kubectl`, then allow you tooexplore hello deployment through hello Kubernetes web interface.</span></span>

### <a name="deploy-with-hello-kubernetes-web-interface"></a><span data-ttu-id="dff7d-156">Met de Hallo Kubernetes web-interface implementeren</span><span class="sxs-lookup"><span data-stu-id="dff7d-156">Deploy with hello Kubernetes web interface</span></span>

1. <span data-ttu-id="dff7d-157">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="dff7d-157">Open a command prompt.</span></span>

1. <span data-ttu-id="dff7d-158">Hallo configuratie website voor uw cluster Kubernetes openen in de standaardbrowser:</span><span class="sxs-lookup"><span data-stu-id="dff7d-158">Open hello configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="dff7d-159">Wanneer Hallo Kubernetes configuratie website in uw browser wordt geopend, klikt u op Hallo koppeling te**een beperkte app implementeren**:</span><span class="sxs-lookup"><span data-stu-id="dff7d-159">When hello Kubernetes configuration website opens in your browser, click hello link too**deploy a containerized app**:</span></span>

   ![Kubernetes configuratie Website][KB01]

1. <span data-ttu-id="dff7d-161">Wanneer Hallo **een beperkte app implementeren** pagina wordt weergegeven, geeft u Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="dff7d-161">When hello **Deploy a containerized app** page is displayed, specify hello following options:</span></span>

   <span data-ttu-id="dff7d-162">a.</span><span class="sxs-lookup"><span data-stu-id="dff7d-162">a.</span></span> <span data-ttu-id="dff7d-163">Selecteer **appdetails hieronder opgeven**.</span><span class="sxs-lookup"><span data-stu-id="dff7d-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="dff7d-164">b.</span><span class="sxs-lookup"><span data-stu-id="dff7d-164">b.</span></span> <span data-ttu-id="dff7d-165">Voer de naam van uw Spring Boot-toepassing voor Hallo **appnaam**; bijvoorbeeld: '*gs-spring-boot-docker*'.</span><span class="sxs-lookup"><span data-stu-id="dff7d-165">Enter your Spring Boot application name for hello **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="dff7d-166">c.</span><span class="sxs-lookup"><span data-stu-id="dff7d-166">c.</span></span> <span data-ttu-id="dff7d-167">Voer uw aanmelding server en de container installatiekopie van eerder voor Hallo **Container installatiekopie**; bijvoorbeeld: '*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*'.</span><span class="sxs-lookup"><span data-stu-id="dff7d-167">Enter your login server and container image from earlier for hello **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="dff7d-168">d.</span><span class="sxs-lookup"><span data-stu-id="dff7d-168">d.</span></span> <span data-ttu-id="dff7d-169">Kies **externe** voor Hallo **Service**.</span><span class="sxs-lookup"><span data-stu-id="dff7d-169">Choose **External** for hello **Service**.</span></span>

   <span data-ttu-id="dff7d-170">e.</span><span class="sxs-lookup"><span data-stu-id="dff7d-170">e.</span></span> <span data-ttu-id="dff7d-171">Geef uw interne en externe poorten in Hallo **poort** en **poort doel** tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="dff7d-171">Specify your external and internal ports in hello **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes configuratie Website][KB02]


1. <span data-ttu-id="dff7d-173">Klik op **implementeren** toodeploy Hallo container.</span><span class="sxs-lookup"><span data-stu-id="dff7d-173">Click **Deploy** toodeploy hello container.</span></span>

   ![Container implementeren][KB05]

1. <span data-ttu-id="dff7d-175">Wanneer uw toepassing is geïmplementeerd, ziet u uw toepassing Spring Boot is vermeld in **Services**.</span><span class="sxs-lookup"><span data-stu-id="dff7d-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes Services][KB06]

1. <span data-ttu-id="dff7d-177">Als u klikt op de koppeling Hallo voor **externe eindpunten**, ziet u uw toepassing Spring opstarten op Azure.</span><span class="sxs-lookup"><span data-stu-id="dff7d-177">If you click hello link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes Services][KB07]

   ![Voorbeeld-App in Azure bladeren][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="dff7d-180">Met kubectl implementeren</span><span class="sxs-lookup"><span data-stu-id="dff7d-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="dff7d-181">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="dff7d-181">Open a command prompt.</span></span>

1. <span data-ttu-id="dff7d-182">De container in Hallo Kubernetes cluster worden uitgevoerd met behulp van Hallo `kubectl run` opdracht.</span><span class="sxs-lookup"><span data-stu-id="dff7d-182">Run your container in hello Kubernetes cluster by using hello `kubectl run` command.</span></span> <span data-ttu-id="dff7d-183">Geef een servicenaam voor uw app in Kubernetes en de naam van de volledige installatiekopie Hallo.</span><span class="sxs-lookup"><span data-stu-id="dff7d-183">Give a service name for your app in Kubernetes and hello full image name.</span></span> <span data-ttu-id="dff7d-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dff7d-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="dff7d-185">In deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="dff7d-185">In this command:</span></span>

   * <span data-ttu-id="dff7d-186">Hallo-containernaam `gs-spring-boot-docker` is opgegeven onmiddellijk na Hallo `run` opdracht</span><span class="sxs-lookup"><span data-stu-id="dff7d-186">hello container name `gs-spring-boot-docker` is specified immediately after hello `run` command</span></span>

   * <span data-ttu-id="dff7d-187">Hallo `--image` parameter geeft u op Hallo gecombineerde login-server en de naam van de installatiekopie als`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="dff7d-187">hello `--image` parameter specifies hello combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="dff7d-188">Uw cluster Kubernetes blootstellen extern via Hallo `kubectl expose` opdracht.</span><span class="sxs-lookup"><span data-stu-id="dff7d-188">Expose your Kubernetes cluster externally by using hello `kubectl expose` command.</span></span> <span data-ttu-id="dff7d-189">Geef de servicenaam van uw, Hallo openbare TCP-poort die wordt gebruikt tooaccess Hallo app en interne doelpoort Hallo die uw app luistert op.</span><span class="sxs-lookup"><span data-stu-id="dff7d-189">Specify your service name, hello public-facing TCP port used tooaccess hello app, and hello internal target port your app listens on.</span></span> <span data-ttu-id="dff7d-190">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dff7d-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="dff7d-191">In deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="dff7d-191">In this command:</span></span>

   * <span data-ttu-id="dff7d-192">Hallo-containernaam `gs-spring-boot-docker` is opgegeven onmiddellijk na Hallo `expose deployment` opdracht</span><span class="sxs-lookup"><span data-stu-id="dff7d-192">hello container name `gs-spring-boot-docker` is specified immediately after hello `expose deployment` command</span></span>

   * <span data-ttu-id="dff7d-193">Hallo `--type` parameter geeft u op dat cluster Hallo maakt gebruik van load balancer</span><span class="sxs-lookup"><span data-stu-id="dff7d-193">hello `--type` parameter specifies that hello cluster uses load balancer</span></span>

   * <span data-ttu-id="dff7d-194">Hallo `--port` parameter geeft Hallo openbare TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="dff7d-194">hello `--port` parameter specifies hello public-facing TCP port of 80.</span></span> <span data-ttu-id="dff7d-195">U toegang tot de app Hallo op deze poort.</span><span class="sxs-lookup"><span data-stu-id="dff7d-195">You access hello app on this port.</span></span>

   * <span data-ttu-id="dff7d-196">Hallo `--target-port` parameter geeft Hallo interne TCP-poort van 8080.</span><span class="sxs-lookup"><span data-stu-id="dff7d-196">hello `--target-port` parameter specifies hello internal TCP port of 8080.</span></span> <span data-ttu-id="dff7d-197">Hallo load balancer verzendt aanvragen tooyour app op deze poort.</span><span class="sxs-lookup"><span data-stu-id="dff7d-197">hello load balancer forwards requests tooyour app on this port.</span></span>

1. <span data-ttu-id="dff7d-198">Zodra het Hallo-app wordt geïmplementeerd wordt toohello cluster, Hallo externe IP-adres zoeken en openen in uw webbrowser:</span><span class="sxs-lookup"><span data-stu-id="dff7d-198">Once hello app is deployed toohello cluster, query hello external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Voorbeeld-App in Azure bladeren][SB02]


## <a name="next-steps"></a><span data-ttu-id="dff7d-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dff7d-200">Next steps</span></span>

<span data-ttu-id="dff7d-201">Zie voor meer informatie over het gebruik van opstarten Spring op Azure Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dff7d-201">For more information about using Spring Boot on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="dff7d-202">Een versie die voorjaar opstarten toepassing toohello Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="dff7d-202">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="dff7d-203">Een toepassing Spring opstarten op Linux in hello Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="dff7d-203">Deploy a Spring Boot application on Linux in hello Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="dff7d-204">Zie voor meer informatie over het gebruik van Azure met Java Hallo [Azure Java Developer Center] en Hallo [Java-Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="dff7d-204">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="dff7d-205">Zie voor meer informatie over Hallo Spring opstarten op Docker-voorbeeldproject [Spring opstarten op het Docker aan de slag].</span><span class="sxs-lookup"><span data-stu-id="dff7d-205">For more information about hello Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="dff7d-206">Hallo volgende koppelingen bieden aanvullende informatie over het maken van opstarten Spring toepassingen:</span><span class="sxs-lookup"><span data-stu-id="dff7d-206">hello following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="dff7d-207">Zie voor meer informatie over het maken van een eenvoudige Spring Boot-toepassing hello Spring Initializr op https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="dff7d-207">For more information about creating a simple Spring Boot application, see hello Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="dff7d-208">Hallo vindt volgende koppelingen u meer informatie over het gebruik van Kubernetes met Azure:</span><span class="sxs-lookup"><span data-stu-id="dff7d-208">hello following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="dff7d-209">Aan de slag met een cluster Kubernetes in Container Service</span><span class="sxs-lookup"><span data-stu-id="dff7d-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="dff7d-210">Met behulp van Hallo Kubernetes-webgebruikersinterface met Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="dff7d-210">Using hello Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="dff7d-211">Meer informatie over het gebruik van de opdrachtregelinterface Kubernetes is beschikbaar in Hallo **kubectl** gebruikershandleiding op <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="dff7d-211">More information about using Kubernetes command-line interface is available in hello **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="dff7d-212">Hallo Kubernetes website heeft verschillende artikelen waarin met afbeeldingen in persoonlijke registers worden besproken:</span><span class="sxs-lookup"><span data-stu-id="dff7d-212">hello Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="dff7d-213">[Configureren van Service-Accounts voor het gehele product]</span><span class="sxs-lookup"><span data-stu-id="dff7d-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="dff7d-214">[Naamruimten]</span><span class="sxs-lookup"><span data-stu-id="dff7d-214">[Namespaces]</span></span>
* <span data-ttu-id="dff7d-215">[Binnenhalen van een installatiekopie van een persoonlijke register]</span><span class="sxs-lookup"><span data-stu-id="dff7d-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="dff7d-216">Zie voor meer voorbeelden van hoe toouse aangepaste Docker met Azure afbeeldingen [met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux].</span><span class="sxs-lookup"><span data-stu-id="dff7d-216">For additional examples for how toouse custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java-Tools voor Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Configureren van Service-Accounts voor het gehele product]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Naamruimten]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Binnenhalen van een installatiekopie van een persoonlijke register]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
