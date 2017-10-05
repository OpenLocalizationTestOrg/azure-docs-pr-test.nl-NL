---
title: Een App Spring opstarten op Kubernetes in Azure Containerservice implementeren | Microsoft Docs
description: Deze zelfstudie leert u Hoewel de stappen voor het implementeren van een toepassing Spring opstarten in een Kubernetes cluster op Microsoft Azure.
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
ms.openlocfilehash: 7f726436b2d459b8c16abb02e07de099abfd8974
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-the-azure-container-service"></a><span data-ttu-id="e2148-103">Een Spring Boot-toepassing implementeren op een Kubernetes-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e2148-103">Deploy a Spring Boot Application on a Kubernetes Cluster in the Azure Container Service</span></span>

<span data-ttu-id="e2148-104">De  **[Spring Framework]**  is een populaire open-source framework waarmee ontwikkelaars van Java web, mobiel en API-toepassingen maken.</span><span class="sxs-lookup"><span data-stu-id="e2148-104">The **[Spring Framework]** is a popular open-source framework that helps Java developers create web, mobile, and API applications.</span></span> <span data-ttu-id="e2148-105">In deze zelfstudie wordt een voorbeeld-app gemaakt met behulp van [Spring Boot], een conventie voor gestuurde benadering voor het gebruik van Spring snel aan de slag.</span><span class="sxs-lookup"><span data-stu-id="e2148-105">This tutorial uses a sample app created using [Spring Boot], a convention-driven approach for using Spring to get started quickly.</span></span>

<span data-ttu-id="e2148-106">**[Kubernetes]**  en  **[Docker]**  zijn open source-oplossingen die ontwikkelaars helpen bij het automatiseren van de implementatie, schaalbaarheid en beheer van hun toepassingen die worden uitgevoerd containers.</span><span class="sxs-lookup"><span data-stu-id="e2148-106">**[Kubernetes]** and **[Docker]** are open-source solutions that help developers automate the deployment, scaling, and management of their applications  running in containers.</span></span>

<span data-ttu-id="e2148-107">Deze zelfstudie wordt u al het combineren van deze twee populaire open-source technologieën voor het ontwikkelen en implementeren van een toepassing Spring opstarten naar Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e2148-107">This tutorial walks you though combining these two popular, open-source technologies to develop and deploy a Spring Boot application to Microsoft Azure.</span></span> <span data-ttu-id="e2148-108">Meer specifiek, gebruikt u  *[Spring Boot]*  voor toepassingsontwikkeling,  *[Kubernetes]*  voor implementatie van de container en de [ Azure Container Service (ACS)] voor het hosten van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="e2148-108">More specifically, you use *[Spring Boot]* for application development, *[Kubernetes]* for container deployment, and the [Azure Container Service (ACS)] to host your application.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e2148-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2148-109">Prerequisites</span></span>

* <span data-ttu-id="e2148-110">Een Azure-abonnement; Als u nog geen Azure-abonnement hebt, kunt u activeren uw [voordelen als MSDN-abonnee] of zich aanmelden voor een [gratis Azure-account].</span><span class="sxs-lookup"><span data-stu-id="e2148-110">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>
* <span data-ttu-id="e2148-111">De [Azure-opdrachtregelinterface (CLI)].</span><span class="sxs-lookup"><span data-stu-id="e2148-111">The [Azure Command-Line Interface (CLI)].</span></span>
* <span data-ttu-id="e2148-112">Een up-to-date [Java Developer Kit (JDK)].</span><span class="sxs-lookup"><span data-stu-id="e2148-112">An up-to-date [Java Developer Kit (JDK)].</span></span>
* <span data-ttu-id="e2148-113">Apache van [Maven] bouwen tool (versie 3).</span><span class="sxs-lookup"><span data-stu-id="e2148-113">Apache's [Maven] build tool (Version 3).</span></span>
* <span data-ttu-id="e2148-114">Een [Git] client.</span><span class="sxs-lookup"><span data-stu-id="e2148-114">A [Git] client.</span></span>
* <span data-ttu-id="e2148-115">Een [Docker] client.</span><span class="sxs-lookup"><span data-stu-id="e2148-115">A [Docker] client.</span></span>

> [!NOTE]
>
> <span data-ttu-id="e2148-116">Vanwege de virtualisatie-vereisten van deze zelfstudie, kan niet u de stappen in dit artikel volgen op een virtuele machine; u moet een fysieke computer gebruiken met virtualisatiefuncties ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e2148-116">Due to the virtualization requirements of this tutorial, you cannot follow the steps in this article on a virtual machine; you must use a physical computer with virtualization features enabled.</span></span>
>

## <a name="create-the-spring-boot-on-docker-getting-started-web-app"></a><span data-ttu-id="e2148-117">Maken van de opstartinstallatiekopie Spring op web-app Docker aan de slag</span><span class="sxs-lookup"><span data-stu-id="e2148-117">Create the Spring Boot on Docker Getting Started web app</span></span>

<span data-ttu-id="e2148-118">De volgende stappen maakt u bij het bouwen van een webtoepassing Spring opstarten en lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="e2148-118">The following steps walk you through building a Spring Boot web application and testing it locally.</span></span>

1. <span data-ttu-id="e2148-119">Open een opdrachtprompt en maak een lokale map houdt uw toepassing en wijzig in die map; bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2148-119">Open a command-prompt and create a local directory to hold your application, and change to that directory; for example:</span></span>
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   <span data-ttu-id="e2148-120">-- of--</span><span class="sxs-lookup"><span data-stu-id="e2148-120">-- or --</span></span>
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. <span data-ttu-id="e2148-121">Kloon de [Spring opstarten op het Docker aan de slag] voorbeeldproject naar de map.</span><span class="sxs-lookup"><span data-stu-id="e2148-121">Clone the [Spring Boot on Docker Getting Started] sample project into the directory.</span></span>
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. <span data-ttu-id="e2148-122">Wijzig de directory aan het voltooide project.</span><span class="sxs-lookup"><span data-stu-id="e2148-122">Change directory to the completed project.</span></span>
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. <span data-ttu-id="e2148-123">Maven gebruiken om te bouwen en uitvoeren van de voorbeeld-app.</span><span class="sxs-lookup"><span data-stu-id="e2148-123">Use Maven to build and run the sample app.</span></span>
   ```
   mvn package spring-boot:run
   ```

1. <span data-ttu-id="e2148-124">De web-app testen door te bladeren naar http://localhost: 8080 of met de volgende `curl` opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2148-124">Test the web app by browsing to http://localhost:8080, or with the following `curl` command:</span></span>
   ```
   curl http://localhost:8080
   ```

1. <span data-ttu-id="e2148-125">U ziet het volgende bericht weergegeven: **Docker HelloWorld**</span><span class="sxs-lookup"><span data-stu-id="e2148-125">You should see the following message displayed: **Hello Docker World**</span></span>

   ![Lokaal voorbeeld-App bladeren][SB01]

## <a name="create-an-azure-container-registry-using-the-azure-cli"></a><span data-ttu-id="e2148-127">Maken van een Azure Container register met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2148-127">Create an Azure Container Registry using the Azure CLI</span></span>

1. <span data-ttu-id="e2148-128">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e2148-128">Open a command prompt.</span></span>

1. <span data-ttu-id="e2148-129">Aanmelden bij uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="e2148-129">Log in to your Azure account:</span></span>
   ```azurecli
   az login
   ```

1. <span data-ttu-id="e2148-130">Maak een resourcegroep voor de Azure-resources in deze zelfstudie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2148-130">Create a resource group for the Azure resources used in this tutorial.</span></span>
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. <span data-ttu-id="e2148-131">Maak een register persoonlijke Azure-container in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e2148-131">Create a private Azure container registry in the resource group.</span></span> <span data-ttu-id="e2148-132">De zelfstudie duwt de voorbeeld-app als een Docker-installatiekopie in dit register in latere stappen.</span><span class="sxs-lookup"><span data-stu-id="e2148-132">The tutorial pushes the sample app as a Docker image to this registry in later steps.</span></span> <span data-ttu-id="e2148-133">Vervang `wingtiptoysregistry` met een unieke naam voor het register.</span><span class="sxs-lookup"><span data-stu-id="e2148-133">Replace `wingtiptoysregistry` with a unique name for your registry.</span></span>
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-to-the-container-registry"></a><span data-ttu-id="e2148-134">Uw app in het register van de container push</span><span class="sxs-lookup"><span data-stu-id="e2148-134">Push your app to the container registry</span></span>

1. <span data-ttu-id="e2148-135">Navigeer naar de configuratiemap voor uw installatie Maven (standaard ~/.m2/ of C:\Users\username\.m2) en open de *settings.xml* bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="e2148-135">Navigate to the configuration directory for your Maven installation (default ~/.m2/ or C:\Users\username\.m2) and open the *settings.xml* file with a text editor.</span></span>

1. <span data-ttu-id="e2148-136">Het wachtwoord voor uw register container ophalen met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e2148-136">Retrieve the password for your container registry from the Azure CLI.</span></span>
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. <span data-ttu-id="e2148-137">Uw Azure-Container register-id en wachtwoord toevoegen aan een nieuwe `<server>` verzameling in de *settings.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="e2148-137">Add your Azure Container Registry id and password to a new `<server>` collection in the *settings.xml* file.</span></span>
<span data-ttu-id="e2148-138">De `id` en `username` zijn de naam van het register.</span><span class="sxs-lookup"><span data-stu-id="e2148-138">The `id` and `username` are the name of the registry.</span></span> <span data-ttu-id="e2148-139">Gebruik de `password` waarde uit de vorige opdracht (zonder aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="e2148-139">Use the `password` value from the previous command (without quotes).</span></span>

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. <span data-ttu-id="e2148-140">Ga naar de map voltooid project voor uw toepassing Spring opstarten (bijvoorbeeld '*C:\SpringBoot\gs-spring-boot-docker\complete*"of"*/users/robert/SpringBoot/gs-spring-boot-docker/complete* '), en open de *pom.xml* bestand met een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="e2148-140">Navigate to the completed project directory for your Spring Boot application (for example, "*C:\SpringBoot\gs-spring-boot-docker\complete*" or "*/users/robert/SpringBoot/gs-spring-boot-docker/complete*"), and open the *pom.xml* file with a text editor.</span></span>

1. <span data-ttu-id="e2148-141">Update de `<properties>` verzameling in de *pom.xml* -bestand met de waarde van de server aanmelding voor uw Azure-Container-register.</span><span class="sxs-lookup"><span data-stu-id="e2148-141">Update the `<properties>` collection in the *pom.xml* file with the login server value for your Azure Container Registry.</span></span>

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. <span data-ttu-id="e2148-142">Update de `<plugins>` verzameling in de *pom.xml* bestand zodat de `<plugin>` bevat van de server en het register aanmeldingsnaam voor uw Azure-Container-register.</span><span class="sxs-lookup"><span data-stu-id="e2148-142">Update the `<plugins>` collection in the *pom.xml* file so that the `<plugin>` contains the login server address and registry name for your Azure Container Registry.</span></span>

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

1. <span data-ttu-id="e2148-143">Ga naar de map voltooid project voor uw toepassing Spring opstarten en voer de volgende opdracht voor het bouwen van de Docker-container en de installatiekopie van het push naar het register:</span><span class="sxs-lookup"><span data-stu-id="e2148-143">Navigate to the completed project directory for your Spring Boot application and run the following command to build the Docker container and push the image to the registry:</span></span>

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  <span data-ttu-id="e2148-144">Er wordt een foutbericht weergegeven dat vergelijkbaar is met een van de volgende wanneer u Maven duwt de installatiekopie naar Azure:</span><span class="sxs-lookup"><span data-stu-id="e2148-144">You may receive an error message that is similar to one of the following when Maven pushes the image to Azure:</span></span>
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed to execute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> <span data-ttu-id="e2148-145">Als u deze fout krijgt, meld u aan bij Azure vanaf de opdrachtregel Docker.</span><span class="sxs-lookup"><span data-stu-id="e2148-145">If you get this error, log in to Azure from the Docker command line.</span></span>
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> <span data-ttu-id="e2148-146">Vervolgens push uw container:</span><span class="sxs-lookup"><span data-stu-id="e2148-146">Then push your container:</span></span>
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-the-azure-cli"></a><span data-ttu-id="e2148-147">Maak een Kubernetes Cluster op ACS met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e2148-147">Create a Kubernetes Cluster on ACS using the Azure CLI</span></span>

1. <span data-ttu-id="e2148-148">Maak een Kubernetes-cluster in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="e2148-148">Create a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="e2148-149">De volgende opdracht maakt u een *kubernetes* -cluster in de *wingtiptoys kubernetes* resource groep met *wingtiptoys containerservice* als de naam van het cluster, en *wingtiptoys kubernetes* als de DNS-voorvoegsel:</span><span class="sxs-lookup"><span data-stu-id="e2148-149">The following command creates a *kubernetes* cluster in the *wingtiptoys-kubernetes* resource group, with *wingtiptoys-containerservice* as the cluster name, and *wingtiptoys-kubernetes* as the DNS prefix:</span></span>
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   <span data-ttu-id="e2148-150">Met deze opdracht kan even duren om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="e2148-150">This command may take a while to complete.</span></span>

1. <span data-ttu-id="e2148-151">Installeer `kubectl` met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e2148-151">Install `kubectl` using the Azure CLI.</span></span> <span data-ttu-id="e2148-152">Linux-gebruikers hebben mogelijk tot het voorvoegsel van deze opdracht met `sudo` sinds deze de CLI Kubernetes naar implementeert `/usr/local/bin`.</span><span class="sxs-lookup"><span data-stu-id="e2148-152">Linux users may have to prefix this command with `sudo` since it deploys the Kubernetes CLI to `/usr/local/bin`.</span></span>
   ```azurecli
   az acs kubernetes install-cli
   ```

1. <span data-ttu-id="e2148-153">Downloaden van de configuratie-informatie van het cluster zodat u uw cluster vanuit de webinterface Kubernetes beheren kunt en `kubectl`.</span><span class="sxs-lookup"><span data-stu-id="e2148-153">Download the cluster configuration information so you can manage your cluster from the Kubernetes web interface and `kubectl`.</span></span> 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-the-image-to-your-kubernetes-cluster"></a><span data-ttu-id="e2148-154">De installatiekopie implementeren op uw cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e2148-154">Deploy the image to your Kubernetes cluster</span></span>

<span data-ttu-id="e2148-155">Deze zelfstudie implementeert u de app met behulp `kubectl`, klikt u vervolgens kunt u de implementatie via de webinterface Kubernetes verkennen.</span><span class="sxs-lookup"><span data-stu-id="e2148-155">This tutorial deploys the app using `kubectl`, then allow you to explore the deployment through the Kubernetes web interface.</span></span>

### <a name="deploy-with-the-kubernetes-web-interface"></a><span data-ttu-id="e2148-156">Met de webinterface Kubernetes implementeren</span><span class="sxs-lookup"><span data-stu-id="e2148-156">Deploy with the Kubernetes web interface</span></span>

1. <span data-ttu-id="e2148-157">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e2148-157">Open a command prompt.</span></span>

1. <span data-ttu-id="e2148-158">Open de website van de configuratie voor uw cluster Kubernetes in de browser:</span><span class="sxs-lookup"><span data-stu-id="e2148-158">Open the configuration website for your Kubernetes cluster in your default browser:</span></span>
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. <span data-ttu-id="e2148-159">Als de website van de configuratie Kubernetes in uw browser wordt geopend, klikt u op de koppeling naar **een beperkte app implementeren**:</span><span class="sxs-lookup"><span data-stu-id="e2148-159">When the Kubernetes configuration website opens in your browser, click the link to **deploy a containerized app**:</span></span>

   ![Kubernetes configuratie Website][KB01]

1. <span data-ttu-id="e2148-161">Wanneer de **een beperkte app implementeren** pagina wordt weergegeven, geeft u de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="e2148-161">When the **Deploy a containerized app** page is displayed, specify the following options:</span></span>

   <span data-ttu-id="e2148-162">a.</span><span class="sxs-lookup"><span data-stu-id="e2148-162">a.</span></span> <span data-ttu-id="e2148-163">Selecteer **appdetails hieronder opgeven**.</span><span class="sxs-lookup"><span data-stu-id="e2148-163">Select **Specify app details below**.</span></span>

   <span data-ttu-id="e2148-164">b.</span><span class="sxs-lookup"><span data-stu-id="e2148-164">b.</span></span> <span data-ttu-id="e2148-165">Voer de naam van uw Spring Boot-toepassing voor de **appnaam**; bijvoorbeeld: '*gs-spring-boot-docker*'.</span><span class="sxs-lookup"><span data-stu-id="e2148-165">Enter your Spring Boot application name for the **App name**; for example: "*gs-spring-boot-docker*".</span></span>

   <span data-ttu-id="e2148-166">c.</span><span class="sxs-lookup"><span data-stu-id="e2148-166">c.</span></span> <span data-ttu-id="e2148-167">Voer uw aanmelding server en de container afbeelding van eerder voor de **Container installatiekopie**; bijvoorbeeld: '*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*'.</span><span class="sxs-lookup"><span data-stu-id="e2148-167">Enter your login server and container image from earlier for the **Container image**; for example: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".</span></span>

   <span data-ttu-id="e2148-168">d.</span><span class="sxs-lookup"><span data-stu-id="e2148-168">d.</span></span> <span data-ttu-id="e2148-169">Kies **externe** voor de **Service**.</span><span class="sxs-lookup"><span data-stu-id="e2148-169">Choose **External** for the **Service**.</span></span>

   <span data-ttu-id="e2148-170">e.</span><span class="sxs-lookup"><span data-stu-id="e2148-170">e.</span></span> <span data-ttu-id="e2148-171">Geef uw interne en externe poorten in de **poort** en **poort doel** tekstvakken.</span><span class="sxs-lookup"><span data-stu-id="e2148-171">Specify your external and internal ports in the **Port** and **Target port** text boxes.</span></span>

   ![Kubernetes configuratie Website][KB02]


1. <span data-ttu-id="e2148-173">Klik op **implementeren** voor het implementeren van de container.</span><span class="sxs-lookup"><span data-stu-id="e2148-173">Click **Deploy** to deploy the container.</span></span>

   ![Container implementeren][KB05]

1. <span data-ttu-id="e2148-175">Wanneer uw toepassing is geïmplementeerd, ziet u uw toepassing Spring Boot is vermeld in **Services**.</span><span class="sxs-lookup"><span data-stu-id="e2148-175">Once your application has been deployed, you will see your Spring Boot application listed under **Services**.</span></span>

   ![Kubernetes Services][KB06]

1. <span data-ttu-id="e2148-177">Als u op de koppeling voor **externe eindpunten**, ziet u uw toepassing Spring opstarten op Azure.</span><span class="sxs-lookup"><span data-stu-id="e2148-177">If you click the link for **External endpoints**, you can see your Spring Boot application running on Azure.</span></span>

   ![Kubernetes Services][KB07]

   ![Voorbeeld-App in Azure bladeren][SB02]


### <a name="deploy-with-kubectl"></a><span data-ttu-id="e2148-180">Met kubectl implementeren</span><span class="sxs-lookup"><span data-stu-id="e2148-180">Deploy with kubectl</span></span>

1. <span data-ttu-id="e2148-181">Open een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e2148-181">Open a command prompt.</span></span>

1. <span data-ttu-id="e2148-182">De container in het cluster Kubernetes uitvoeren met behulp van de `kubectl run` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e2148-182">Run your container in the Kubernetes cluster by using the `kubectl run` command.</span></span> <span data-ttu-id="e2148-183">Geef een servicenaam voor uw app in Kubernetes en naam van de volledige installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="e2148-183">Give a service name for your app in Kubernetes and the full image name.</span></span> <span data-ttu-id="e2148-184">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2148-184">For example:</span></span>
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   <span data-ttu-id="e2148-185">In deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2148-185">In this command:</span></span>

   * <span data-ttu-id="e2148-186">De containernaam `gs-spring-boot-docker` is opgegeven onmiddellijk na de `run` opdracht</span><span class="sxs-lookup"><span data-stu-id="e2148-186">The container name `gs-spring-boot-docker` is specified immediately after the `run` command</span></span>

   * <span data-ttu-id="e2148-187">De `--image` parameter geeft u de gecombineerde server- en afbeeldingsbestanden aanmeldingsnaam als`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span><span class="sxs-lookup"><span data-stu-id="e2148-187">The `--image` parameter specifies the combined login server and image name as `wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`</span></span>

1. <span data-ttu-id="e2148-188">Uw cluster Kubernetes blootstellen extern met behulp van de `kubectl expose` opdracht.</span><span class="sxs-lookup"><span data-stu-id="e2148-188">Expose your Kubernetes cluster externally by using the `kubectl expose` command.</span></span> <span data-ttu-id="e2148-189">Geef de servicenaam van uw, de openbare TCP-poort gebruikt voor toegang tot de app en de interne doelpoort die uw app luistert op.</span><span class="sxs-lookup"><span data-stu-id="e2148-189">Specify your service name, the public-facing TCP port used to access the app, and the internal target port your app listens on.</span></span> <span data-ttu-id="e2148-190">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2148-190">For example:</span></span>
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   <span data-ttu-id="e2148-191">In deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="e2148-191">In this command:</span></span>

   * <span data-ttu-id="e2148-192">De containernaam `gs-spring-boot-docker` is opgegeven onmiddellijk na de `expose deployment` opdracht</span><span class="sxs-lookup"><span data-stu-id="e2148-192">The container name `gs-spring-boot-docker` is specified immediately after the `expose deployment` command</span></span>

   * <span data-ttu-id="e2148-193">De `--type` parameter geeft u op dat de cluster maakt gebruik van load balancer</span><span class="sxs-lookup"><span data-stu-id="e2148-193">The `--type` parameter specifies that the cluster uses load balancer</span></span>

   * <span data-ttu-id="e2148-194">De `--port` parameter geeft u de openbare TCP-poort 80.</span><span class="sxs-lookup"><span data-stu-id="e2148-194">The `--port` parameter specifies the public-facing TCP port of 80.</span></span> <span data-ttu-id="e2148-195">U toegang tot de app op deze poort.</span><span class="sxs-lookup"><span data-stu-id="e2148-195">You access the app on this port.</span></span>

   * <span data-ttu-id="e2148-196">De `--target-port` parameter geeft u op de interne TCP-poort van 8080.</span><span class="sxs-lookup"><span data-stu-id="e2148-196">The `--target-port` parameter specifies the internal TCP port of 8080.</span></span> <span data-ttu-id="e2148-197">De load balancer verzendt aanvragen naar uw app op deze poort.</span><span class="sxs-lookup"><span data-stu-id="e2148-197">The load balancer forwards requests to your app on this port.</span></span>

1. <span data-ttu-id="e2148-198">Zodra de app is geïmplementeerd met het cluster, het externe IP-adres zoeken en openen in uw webbrowser:</span><span class="sxs-lookup"><span data-stu-id="e2148-198">Once the app is deployed to the cluster, query the external IP address and open it in your web browser:</span></span>

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Voorbeeld-App in Azure bladeren][SB02]


## <a name="next-steps"></a><span data-ttu-id="e2148-200">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2148-200">Next steps</span></span>

<span data-ttu-id="e2148-201">Zie de volgende artikelen voor meer informatie over het gebruik van opstarten Spring op Azure:</span><span class="sxs-lookup"><span data-stu-id="e2148-201">For more information about using Spring Boot on Azure, see the following articles:</span></span>

* [<span data-ttu-id="e2148-202">Een toepassing Spring opstart in de Azure App Service implementeren</span><span class="sxs-lookup"><span data-stu-id="e2148-202">Deploy a Spring Boot Application to the Azure App Service</span></span>](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [<span data-ttu-id="e2148-203">Een toepassing Spring opstarten op Linux in de Azure Container Service implementeren</span><span class="sxs-lookup"><span data-stu-id="e2148-203">Deploy a Spring Boot application on Linux in the Azure Container Service</span></span>](container-service-deploy-spring-boot-app-on-linux.md)

<span data-ttu-id="e2148-204">Voor meer informatie over het gebruik van Azure met Java raadpleegt u het [Azure Java-ontwikkelaarscentrum] en de [Java Tools voor Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="e2148-204">For more information about using Azure with Java, see the [Azure Java Developer Center] and the [Java Tools for Visual Studio Team Services].</span></span>

<span data-ttu-id="e2148-205">Zie voor meer informatie over het opstarten van de versie die voorjaar op Docker-voorbeeldproject [Spring opstarten op het Docker aan de slag].</span><span class="sxs-lookup"><span data-stu-id="e2148-205">For more information about the Spring Boot on Docker sample project, see [Spring Boot on Docker Getting Started].</span></span>

<span data-ttu-id="e2148-206">De volgende koppelingen vindt aanvullende informatie over het maken van opstarten Spring toepassingen:</span><span class="sxs-lookup"><span data-stu-id="e2148-206">The following links provide additional information about creating Spring Boot applications:</span></span>

* <span data-ttu-id="e2148-207">Zie voor meer informatie over het maken van een eenvoudige Spring Boot-toepassing de Initializr Spring op https://start.spring.io/.</span><span class="sxs-lookup"><span data-stu-id="e2148-207">For more information about creating a simple Spring Boot application, see the Spring Initializr at https://start.spring.io/.</span></span>

<span data-ttu-id="e2148-208">De volgende koppelingen vindt u meer informatie over het gebruik van Kubernetes met Azure:</span><span class="sxs-lookup"><span data-stu-id="e2148-208">The following links provide additional information about using Kubernetes with Azure:</span></span>

* [<span data-ttu-id="e2148-209">Aan de slag met een cluster Kubernetes in Container Service</span><span class="sxs-lookup"><span data-stu-id="e2148-209">Get started with a Kubernetes cluster in Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [<span data-ttu-id="e2148-210">Met behulp van de webgebruikersinterface Kubernetes met Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="e2148-210">Using the Kubernetes web UI with Azure Container Service</span></span>](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

<span data-ttu-id="e2148-211">Meer informatie over het gebruik van de opdrachtregelinterface Kubernetes is beschikbaar in de **kubectl** gebruikershandleiding op <https://kubernetes.io/docs/user-guide/kubectl/>.</span><span class="sxs-lookup"><span data-stu-id="e2148-211">More information about using Kubernetes command-line interface is available in the **kubectl** user guide at <https://kubernetes.io/docs/user-guide/kubectl/>.</span></span>

<span data-ttu-id="e2148-212">De website Kubernetes heeft verschillende artikelen waarin met afbeeldingen in persoonlijke registers worden besproken:</span><span class="sxs-lookup"><span data-stu-id="e2148-212">The Kubernetes website has several articles that discuss using images in private registries:</span></span>

* <span data-ttu-id="e2148-213">[Configureren van Service-Accounts voor het gehele product]</span><span class="sxs-lookup"><span data-stu-id="e2148-213">[Configuring Service Accounts for Pods]</span></span>
* <span data-ttu-id="e2148-214">[Naamruimten]</span><span class="sxs-lookup"><span data-stu-id="e2148-214">[Namespaces]</span></span>
* <span data-ttu-id="e2148-215">[Binnenhalen van een installatiekopie van een persoonlijke register]</span><span class="sxs-lookup"><span data-stu-id="e2148-215">[Pulling an Image from a Private Registry]</span></span>

<span data-ttu-id="e2148-216">Zie voor meer voorbeelden voor het aangepaste Docker-installatiekopieën gebruiken met Azure [met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux].</span><span class="sxs-lookup"><span data-stu-id="e2148-216">For additional examples for how to use custom Docker images with Azure, see [Using a custom Docker image for Azure Web App on Linux].</span></span>

<!-- URL List -->

<span data-ttu-id="e2148-217">[Azure-opdrachtregelinterface (CLI)]: /cli/azure/overview</span><span class="sxs-lookup"><span data-stu-id="e2148-217">[Azure Command-Line Interface (CLI)]: /cli/azure/overview</span></span>
<span data-ttu-id="e2148-218">[ Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span><span class="sxs-lookup"><span data-stu-id="e2148-218">[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/</span></span>
<span data-ttu-id="e2148-219">[Azure Java-ontwikkelaarscentrum]: https://azure.microsoft.com/develop/java/</span><span class="sxs-lookup"><span data-stu-id="e2148-219">[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/</span></span>
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using the Azure portal]: /azure/container-registry/container-registry-get-started-portal
<span data-ttu-id="e2148-220">[met een aangepaste Docker-installatiekopie voor Azure-Web-App op Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span><span class="sxs-lookup"><span data-stu-id="e2148-220">[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image</span></span>
<span data-ttu-id="e2148-221">[Docker]: https://www.docker.com/</span><span class="sxs-lookup"><span data-stu-id="e2148-221">[Docker]: https://www.docker.com/</span></span>
<span data-ttu-id="e2148-222">[gratis Azure-account]: https://azure.microsoft.com/pricing/free-trial/</span><span class="sxs-lookup"><span data-stu-id="e2148-222">[free Azure account]: https://azure.microsoft.com/pricing/free-trial/</span></span>
<span data-ttu-id="e2148-223">[Git]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="e2148-223">[Git]: https://github.com/</span></span>
<span data-ttu-id="e2148-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span><span class="sxs-lookup"><span data-stu-id="e2148-224">[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/</span></span>
<span data-ttu-id="e2148-225">[Java Tools voor Visual Studio Team Services]: https://java.visualstudio.com/</span><span class="sxs-lookup"><span data-stu-id="e2148-225">[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/</span></span>
<span data-ttu-id="e2148-226">[Kubernetes]: https://kubernetes.io/</span><span class="sxs-lookup"><span data-stu-id="e2148-226">[Kubernetes]: https://kubernetes.io/</span></span>
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
<span data-ttu-id="e2148-227">[Maven]: http://maven.apache.org/</span><span class="sxs-lookup"><span data-stu-id="e2148-227">[Maven]: http://maven.apache.org/</span></span>
<span data-ttu-id="e2148-228">[voordelen als MSDN-abonnee]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span><span class="sxs-lookup"><span data-stu-id="e2148-228">[MSDN subscriber benefits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/</span></span>
<span data-ttu-id="e2148-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span><span class="sxs-lookup"><span data-stu-id="e2148-229">[Spring Boot]: http://projects.spring.io/spring-boot/</span></span>
<span data-ttu-id="e2148-230">[Spring opstarten op het Docker aan de slag]: https://github.com/spring-guides/gs-spring-boot-docker</span><span class="sxs-lookup"><span data-stu-id="e2148-230">[Spring Boot on Docker Getting Started]: https://github.com/spring-guides/gs-spring-boot-docker</span></span>
<span data-ttu-id="e2148-231">[Spring Framework]: https://spring.io/</span><span class="sxs-lookup"><span data-stu-id="e2148-231">[Spring Framework]: https://spring.io/</span></span>
<span data-ttu-id="e2148-232">[Configureren van Service-Accounts voor het gehele product]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span><span class="sxs-lookup"><span data-stu-id="e2148-232">[Configuring Service Accounts for Pods]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/</span></span>
<span data-ttu-id="e2148-233">[Naamruimten]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span><span class="sxs-lookup"><span data-stu-id="e2148-233">[Namespaces]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/</span></span>
<span data-ttu-id="e2148-234">[Binnenhalen van een installatiekopie van een persoonlijke register]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span><span class="sxs-lookup"><span data-stu-id="e2148-234">[Pulling an Image from a Private Registry]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/</span></span>

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
